# Cardinalités – MVP Intérim

| # | De | Action | Vers | Cardinalité |
|---|---|---|---|---|
| 1 | USER | a | WORKER | `0,1` |
| 2 | WORKER | appartient à | USER | `1,1` |
| 3 | USER | a | COMPANY | `0,1` |
| 4 | COMPANY | appartient à | USER | `1,1` |
| 5 | COMPANY | publie | MISSION | `0,n` |
| 6 | MISSION | est publiée par | COMPANY | `1,1` |
| 7 | MISSION | reçoit | CANDIDATURE | `0,n` |
| 8 | CANDIDATURE | concerne | MISSION | `1,1` |
| 9 | WORKER | soumet | CANDIDATURE | `0,n` |
| 10 | CANDIDATURE | est soumise par | WORKER | `1,1` |
