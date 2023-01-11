---
title: 🏢 Gerrit
---

### Customized dashboard

```
/dashboard/?title=👨%E2%80%8D💻My+Dashboard&🔔=status:open+(ownerin:my-group+OR+project:my-project)+hashtag:prio&📄=has:draft&🧪=is:open+owner:self+is:wip&📧=is:open+-is:ignored+cc:self&📤=is:open+owner:self+-is:wip+-is:ignored&📥=is:open+(ownerin:my-group+OR+project:my-project)+-owner:self+-is:wip+-is:ignored+-label:Code-Review=2+(reviewer:self+OR+assignee:self)+limit:50
```

### Gmail filters

```
from:(review@domain.tld) -{("Gerrit-Owner: Simon MARQUIS" "Gerrit-HasComments: Yes") "Gerrit-Comment-In-Reply-To: Simon MARQUIS" ("Gerrit-MessageType: setassignee" "Gerrit-Assignee: Simon MARQUIS")}
```
