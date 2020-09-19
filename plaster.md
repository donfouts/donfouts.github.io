# powershell to coordinate the automation of enterprise apps

I am not going to just post my entire script - but will post some snippits that I did struggle to find information on how to do the following actions and perhaps this can save someone some time in the future. 

### Azure table storage / REST opperations

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

this is the block i use to query a table based on the ParitionKey, this is using the access key of the storage account

---

