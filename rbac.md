# RBAC Tables


## Production & Non-Prod

|   | Subscription | Resource group | Service | service-role |
|---|---|---|---|---|
| Devops team admins (psm) |  Owner | Inheritance | Inheritance |   |
| Esp administrators (psm) |   | Owner | Inheritance |   |
| Devops team | Reader  | Contributor   | Inheritance |   |
| Operations | Reader  | Inheritance   | Inheritance |   |
| ESP/ISO | Reader  | Contributor | Contributor |   |
| Senior Developers |   | Reader | Inheritance   | Conditional  |
| Backend Developers  |  | Reader | Inheritance   |   |
| QA engineer |   | Reader | Contributor   | Conditional |
| DBA  | Reader  | Contributor | Inheritance |   |
| UI/UX Developer  |  | Reader | Inheritance | Conditional |
| Scrum Master |  | Reader | Inheritance   |   |
| Managers | Reader | Inheritance | Inheritance   |   |


## Research and Development

|   | Subscription | Resource group | Service | service-role |
|---|---|---|---|---|
| Devops team admins (psm)  | Owner | Inheritance | Inheritance |   |
| Esp administrators (psm)  |  | Owner | Inheritance |  |
| Devops team               | Reader | Contributor | Inheritance |   |
| Operations                | Reader | Inheritance | Inheritance |   |
| ESP/ISO                   | Reader | Contributor | Contributor |   |
| Senior Developers         | Owner | Inheritance | Inheritance | Conditional  |
| Backend Developers        | Contributor | Inheritance | Inheritance |   |
| QA engineer               | Contributor | Reader | Contributor | Conditional |
| DBA                       | Owner | Inheritance  | Inheritance |   |
| UI/UX Developer           | Reader | Contributor | Inheritance | Conditional |
| Scrum Master              | Reader | Contributor | Inheritance |   |
| Managers                  | Owner | Inheritance | Inheritance |   |

