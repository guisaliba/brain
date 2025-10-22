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
