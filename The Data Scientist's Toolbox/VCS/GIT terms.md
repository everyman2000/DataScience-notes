# Some important terms

- Repository/Repo
- Commit
- Push
- Pull
- Staging
- Branch
- Conflict

![[branch.png]]

![[image.png]]

- Clone - Copies repository and changes can be synced to original repo.
- Branch - Git concept. They are always intended to be ‘convergent’ development paths. Branches are ephemeral by their very nature: a branch is really nothing more than a pointer at the head of a commit lineage. Both this pointer and the branch are eventually destroyed and purged from the Git history after the branch is merged into origin/master.
- Fork - When you make a fork, you are duplicating the entire repository and its history up until that point in time. 

==**Forks are best used: when the intent of the ‘split’ is to create a logically independent project, which may never reunite with its parent.**

==**Branches are best used: when they are created as temporary places to work through a feature, with the intent to merge the branch with the origin.**

*A branch-centric workflow makes sense for most business settings. Forks can be a really good pattern for ‘public’ collaboration and experimentation, but when the intended use case is many people working toward a unified goal, branching tends to be a better fit.*

### Healthy habits:
- Purposeful, single issue commits
- Informative commit messages
- Pull and Push often

