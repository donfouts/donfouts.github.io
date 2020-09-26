# powershell to coordinate the automation of web apps

I am not going to just post my entire script - but will post some snippets that I did struggle to find information on how to do the following actions and perhaps this can save someone some time in the future. 

### Azure table storage / REST operations

#### GET

    $storageAccountName = $stacct
    $storageAccountkey = $storagekey
    $tableName = $gtablename
    $apiVersion = "2017-04-17"
    $tableURL = "https://$($storageAccountName).table.core.windows.net/$($tableName)"
    $GMTime = (Get-Date).ToUniversalTime().toString('R')
    $string = "$($GMTime)`n/$($storageAccountName)/$($tableName)"
    $hmacsha = New-Object System.Security.Cryptography.HMACSHA256
    $hmacsha.key = [Convert]::FromBase64String($storageAccountkey)
    $signature = $hmacsha.ComputeHash([Text.Encoding]::UTF8.GetBytes($string))
    $signature = [Convert]::ToBase64String($signature)
    $headers = @{    
        Authorization  = "SharedKeyLite " + $storageAccountName + ":" + $signature
        Accept         = "application/json;odata=fullmetadata"
        'x-ms-date'    = $GMTime
        "x-ms-version" = $apiVersion
    }
    $queryURL = "$($tableURL)?`$filter=(PartitionKey eq 'inventory')"
    $getrequest = Invoke-RestMethod -Method GET -Uri $queryURL -Headers $headers -ContentType application/json

This is the block I use to query a table based on the ParitionKey, this is using the access key of the storage account, I did find this example in a few places online: a few of them seam to be a little different and did not work - as of summer 2020.

---

the results of the azure table are from json and so strings: even the rowkeys: i wanted to sort by rowkey so this is how i handled it:

    $keys = $getrequest.value | Sort-Object {[int]($_.rowkey -replace '(\d+).*', '$1')}

converting the string to the int vault - sort-object works!
another weird problem with the table values being strings, came in when i wanted to work with something like an ID - and for naming sanity wanted leading zeros.
so i had to take the int i was working with in powershell and convert it to a string and add the leading zeros at that time before inserting into azure tables

    $stringID = '{0:d3}' -f [int]$insertbody.ID


#### put

in this example i knew i wanted to update the first key in my results: 

    $update = $keys[0]
    $update.used = "y"
    $update.application = $appname

adding elements i wanted to put into the table entry

    $update.psobject.Properties.Remove('odata.type')
    $update.psobject.Properties.Remove('odata.id')
    $update.psobject.Properties.Remove('odata.etag')
    $update.psobject.Properties.Remove('odata.editlink')
    $update.psobject.Properties.Remove('Timestamp@odata.type')

removed these elements of the table row as they are meta data inserted in the PUT - and I found i needed to remove them so the put would be happy...

    $body = $update | ConvertTo-Json

I found working with powershell object was easier within my code, so most places i received json - i convertfrom-json, and then convertto-json when it needed to be json

    $version = "2017-04-17"
    $resource = "$vnettable(PartitionKey='inventory',RowKey='$workingkey')"
    $table_url = "https://$stacct.table.core.windows.net/$resource"
    $GMTTime = (Get-Date).ToUniversalTime().toString('R')
    $stringToSign = "$GMTTime`n/$stacct/$resource"
    $hmacsha = New-Object System.Security.Cryptography.HMACSHA256
    $hmacsha.key = [Convert]::FromBase64String($storagekey)
    $signature = $hmacsha.ComputeHash([Text.Encoding]::UTF8.GetBytes($stringToSign))
    $signature = [Convert]::ToBase64String($signature)
    $headers = @{
        'x-ms-date'    = $GMTTime
        Authorization  = "SharedKeyLite " + $stacct + ":" + $signature
        "x-ms-version" = $version
        Accept         = "application/json;odata=fullmetadata"
    }

    Invoke-RestMethod -Method PUT -Uri $table_url -Headers $headers -Body $body -ContentType application/json

### let [plaster](https://github.com/PowerShellOrg/Plaster) take over 

to move all of these values into plaster i found this concept of passing a hashtable into the invoke-plaster command, saved tons of time....

    ################
    # insert values into hash table to insert into plaster command
    ################

    $plaster = @{
        azlocname = "$msalocation"
        teamname = "$teamname"
        applicationname = "$appname"
        devvlanid = "$global:devvlanid"
        tstvlanid = "$global:tstvlanid"
        stgvlanid = "$global:stgvlanid"
        prdvlanid = "$global:prdvlanid"
        devnetspace = "$global:devnetspace"
        tstnetspace = "$global:tstnetspace"
        stgnetspace = "$global:stgnetspace"
        prdnetspace = "$global:prdnetspace"
        devwebappid = "$global:devwebappid"
        tstwebappid = "$global:tstwebappid"
        stgwebappid = "$global:stgwebappid"
        prdwebappid = "$global:prdwebappid"
        devrgid = "$global:devrgid"
        tstrgid = "$global:tstrgid"
        stgrgid = "$global:stgrgid"
        prdrgid = "$global:prdrgid"
        devkvid = "$global:devkvid"
        tstkvid = "$global:tstkvid"
        stgkvid = "$global:stgkvid"
        prdkvid = "$global:prdkvid"
    }

    Write-Output "---------------------------------------"
    Write-Output $plaster

    Invoke-Plaster @plaster -DestinationPath .\applications -TemplatePath .\

---
[terraform modules](tfmodules.md)