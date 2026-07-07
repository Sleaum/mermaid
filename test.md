```mermaid
---
merge from myFeature
---
gitGraph
  commit
  commit
  commit
  branch myFeature
  checkout myFeature
  commit
  checkout main
  merge myFeature
```
