## Introduction
Configuration management (CM) in software development is a systems engineering process that tracks and monitors changes to a software system's configuration metadata throughout its lifecycle.

## Historical evolution
Originated in the 1950s as a technical management discipline for hardware development, it has evolved into a foundational practice for modern software engineering.
Programmers in the 1950s and 1960s wrote source code using punch cards, and since no two programmers accessed the same source code simultaneously, there was initially no need for source code control systems.
In 1972, Bell Labs created **Source Code Control System (SCCS)**, written in C by Marc Rochkind. SCCS was the first real version control system, introducing concepts like checkout, commit, and locking systems to avoid conflicts
The 1980s brought the emergence of **Concurrent Versions System (CVS)**, which became widely adopted despite its limitations. Later, **Subversion (SVN)** attempted to address many of CVS's shortcomings while maintaining the centralized model.

### The Distributed Revolution
The development of Git by Linus Torvalds in 2005 marked a watershed moment in configuration management history, marking the shift to Distributed Version Control Systems (DVCS).
Torvalds created Git in response to BitKeeper's license revocation for Linux kernel development.

## Modern branching strategies
### Git Flow
Represents a robust strategy designed for release-based workflows with multiple long-lived branches. It uses five types of branches: main/master (production-ready code), develop (active development), feature (new functionality), release (preparation for production), and hotfix (emergency bug fixes).
### GitHub Flow
Offers a simpler alternative, revolving around a single production-ready main branch with short-lived feature branches. Development work occurs on feature branches, which are merged into main through pull requests that facilitate collaboration and code review.
### Trunk-Based
A single main branch with very short-lived feature branches. Developers frequently merge changes into main, encouraging rapid integration and feedback while minimizing branch management overhead.

## Merge strategies: merge vs. rebase
### Merge
Creates a new commit that combines changes from two branches while preserving the original commit history of both branches.
Merge is non-destructive (existing branches are not changed in any way), making it ideal for collaborative environments where multiple developers contribute to shared branches.
However, merge can create "merge-noise": cluttered history with numerous merge commits.
### Rebase
Rewrites commit history by taking commits from one branch and replaying them on top of another branch, creating a linear, cleaned-up history.
This approach avoid merge commit noise. It is ideal for private feature branches where you're the only developer, when presenting clean commit sequences to your team.
Rebase makes it difficult to track how and when commits where merged though.

## The Linux kernel: A case study in open source CM
The Linux kernel source is managed using Git. There are several key stages: development and contribution, testing, integration, release management, and maintenance.
The kernel follows strict coding standards and requires that patches conform to specific formatting rules.
Patches are submitted to subsystem maintainers who review them on mailing lists, often providing feedback that requires multiple iterations.
The review process may take several rounds before patches are accepted.
### Hierarchical structure
Subsystem maintainers oversee specific areas like memory management, device drivers, and filesystems. Each maintainer has their own Git tree, and changes flow up through this hierarchy until eventually reaching Linus Torvalds's master tree.
After a stable kernel release, a two-week merge window opens where maintainers submit pull requests to Torvalds.

## Google's monorepo
Google's approach is a radical departure from conventional CM, operating one of the world's largest monolithic repositories using a custom version control system (VCS) called **Piper**.
Piper houses most of Google's code—including search, ads, photos, docs/drive, maps, and internal infrastructure—except from Chrome and Android (both are open-source and have their own release schedules).
practices trunk-based development on top of Piper, with the vast majority of users working at the "head" or most recent version of the codebase.
Immediately after any commit, the new code is visible and usable by all developers.
### Supporting tools
Google heavily invested in many supporting tools to make this approach viable.
- CitC (Clients in the Cloud): virtual workspaces in the cloud, devs do not maintain local copies
- Tricorder: automatic checks to provide rapid automated feedback regardless of dev's timezone
- Critique: complex code review framework, with submission, comments and validations
- Pipe: Autoamtic builds triggered by commits after validated by Critique

## Conventional commits
The Conventional Commits specification provides a lightweight convention for creating explicit commit histories, making it easier to write automated tools on top of commit messages.
The standar commit format is:
```
`<type>[optional scope]: <description>

[optional body]

[optional footer(s)]`
```
Common types include:
- feat: Introduces a new feature
- fix: Patches a bug
- docs: Documentation changes only
- style: Formatting changes not affecting code functionality
- refactor: Code restructuring without fixing bugs or adding features
- perf: Performance improvements
- test: Adding or modifying tests
- chore: Changes to build process or auxiliary tools
- ci: Continuous integration configuration changes
- build: Changes affecting the build system or dependencies

## Pull requests
Effective pull request practices form the backbone of collaborative CM:
1. Review your own code before creating the PR
2. Keep PRs small and focused on single features
3. Create draft pull requests for early feedback
4. Use clear, descriptive titles with tags ([Fix], [Feature], [Refactor])
5. Specify required reviewers
When reviewing a pull request, there are also good practices to adhere to:
6. Check for adherence to coding standars
7. Verify test coverage
8. Provide constructive feedback **with solutions**
9. Approve, request changes, or comment

## Software artifacts and build management
Artifact versioning ensures traceability throughout the software development lifecycle.
Build artifacts are the output of the build process, including compiled code, libraries, and resources necessary for running software.
Versioning is crucial