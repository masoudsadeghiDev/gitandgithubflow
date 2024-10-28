# Gitflow Workflow Repository

Git Flow is a popular branching model for Git, designed to help manage and streamline collaborative software development. It introduces a structured workflow for using Git branches in a project, making it easier to handle feature development, releases, and hotfixes. Here's a breakdown of Git Flow's key concepts:

### Main Branches
1. **`main` (or `master`) Branch:**
   - Represents the latest stable version of the project.
   - Only contains production-ready code.
   - New changes are typically merged here through a release or hotfix process.

2. **`develop` Branch:**
   - Serves as the integration branch for features.
   - It contains the latest completed and tested features that are being prepared for the next release.
   - New features are merged into `develop` after being fully implemented and reviewed.

### Supporting Branches
In addition to the main branches, Git Flow defines several supporting branches to organize the work:

1. **Feature Branches (`feature/*`):**
   - Used to develop new features or improvements.
   - Branch off from the `develop` branch.
   - Merged back into `develop` once the feature is complete.
   - Naming convention: `feature/feature-name`.

2. **Release Branches (`release/*`):**
   - Created when preparing a new release.
   - Branch off from `develop` and are used for final testing, bug fixes, and version number updates before the release goes to production.
   - Once complete, the release branch is merged into both `main` and `develop`, and a version tag is added.
   - Naming convention: `release/release-version`.

3. **Hotfix Branches (`hotfix/*`):**
   - Created for critical fixes in the `main` branch that need to be addressed immediately (e.g., production bugs).
   - Branch off from `main` and, after fixing the issue, are merged back into both `main` and `develop`.
   - Naming convention: `hotfix/hotfix-description`.

### Workflow Example
1. **Start a new feature:**
   - Create a new feature branch from `develop`:  
     ```bash
     git checkout develop
     git checkout -b feature/awesome-feature
     ```
   - Implement the feature and commit changes to the feature branch.

2. **Finish the feature:**
   - Merge the feature branch back into `develop`:
     ```bash
     git checkout develop
     git merge feature/awesome-feature
     git branch -d feature/awesome-feature
     ```

3. **Prepare a release:**
   - Create a release branch from `develop`:
     ```bash
     git checkout develop
     git checkout -b release/1.0.0
     ```
   - Perform final testing, make necessary changes, and then merge into both `main` and `develop`:
     ```bash
     git checkout main
     git merge release/1.0.0
     git tag -a 1.0.0
     git checkout develop
     git merge release/1.0.0
     git branch -d release/1.0.0
     ```

4. **Hotfixing:**
   - Create a hotfix branch from `main`:
     ```bash
     git checkout main
     git checkout -b hotfix/urgent-fix
     ```
   - Fix the issue, then merge back into `main` and `develop`:
     ```bash
     git checkout main
     git merge hotfix/urgent-fix
     git tag -a 1.0.1
     git checkout develop
     git merge hotfix/urgent-fix
     git branch -d hotfix/urgent-fix
     ```

### Pros and Cons of Git Flow
#### Pros:
- Clear structure for managing features, releases, and hotfixes.
- Facilitates collaboration and parallel development.
- Simplifies version management through release branches.

#### Cons:
- Can be complex for smaller projects or teams.
- More branches can mean more context switching and merging.
- Not ideal for continuous deployment workflows, as the process may be too rigid.

Git Flow is a good choice for projects with planned release cycles or larger teams where feature segregation is important.