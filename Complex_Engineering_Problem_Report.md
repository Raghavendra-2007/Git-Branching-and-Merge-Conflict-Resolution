# MARWADI UNIVERSITY
## FACULTY OF ENGINEERING AND TECHNOLOGY | DEPARTMENT OF COMPUTER ENGINEERING
### OPEN SOURCE TECHNOLOGIES (01CE0526)
### COMPLEX ENGINEERING PROBLEM - REPORT

---

## TITLE
**GIT BRANCHING AND MERGE CONFLICT RESOLUTION IN DISTRIBUTED VERSION CONTROL SYSTEMS**

- **NAME – 1**: RAGHAVA M [ENROLLMENT: 132049]
- **NAME – 2**: [GROUP MEMBER 2] [ENROLLMENT: 2]
- **NAME – 3**: [GROUP MEMBER 3] [ENROLLMENT: 3]
- **DEPARTMENT**: COMPUTER ENGINEERING
- **ACADEMIC YEAR**: 2026–2027
- **SEMESTER**: 5TH
- **SUBJECT**: OPEN SOURCE TECHNOLOGIES (01CE0526)
- **CLASS**: 5CE
- **BATCH**: Batch 1
- **FACULTY**: Ms. Priyanka Mangi

---

## RUBRICS FOR COMPLEX ENGINEERING PROBLEM

| Sr. No. | Assessment Criteria | Excellent (3 / 4) | Good (2 / 3) | Satisfactory (1 / 1-2) | Poor (0) | Marks |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | **Problem Analysis & Open Source Technology Selection** | Clearly identifies engineering problem, analyzes requirements, selects open source tech with proper justification. (3) | Good analysis with suitable tech selection and minor gaps. (2) | Basic analysis with limited justification. (1) | Inadequate problem analysis and inappropriate selection. (0) | 3 |
| **2** | **System Design, Implementation Strategy & Technical Analysis** | Well-defined system architecture, appropriate stack, version control, and comprehensive technical analysis. (4) | Good system design and technical discussion with minor omissions. (3) | Basic architecture and limited technical analysis. (1–2) | Poor or missing design and analysis. (0) | 4 |
| **3** | **Testing, Documentation & References** | Comprehensive testing strategy, well-organized report, IEEE references, diagrams, and clear conclusions. (3) | Good documentation with minor formatting or testing gaps. (2) | Basic report with limited testing or references. (1) | Incomplete report with poor documentation. (0) | 3 |
| | **Total** | | | | | **10** |

### Evaluation Record
| Sr. No. | Complex Engineering Problem Title | COs | Date | R1(4) | R2(3) | R3(4) | Marks (10) | Signature |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | Git Branching and Merge Conflict Resolution | CO2, CO4 | 05-10-2026 | | | | | |

---

## 1. Aim
To analyse, design, and develop an engineering solution for the given complex engineering problem using appropriate knowledge and tools.

---

## 2. Problem Statement
In modern collaborative software engineering environments, distributed teams concurrently develop features across isolated Git branches. When multiple developers perform divergent modifications on identical lines of code within shared source files, automated merge algorithms fail, precipitating merge conflicts. The objective is to analyze the mechanics of merge conflicts, simulate a concurrent modification scenario between `main` and `feature` branches, perform manual conflict resolution through syntactic and semantic reconciliation, and synchronize the resolved state to a remote GitHub repository.

---

## 3. Problem Analysis

### a) What is the engineering problem?
The engineering problem involves managing non-linear source code divergence in distributed version control systems where concurrent edits to identical lines prevent automated 3-way reconciliation, creating build breakage and workflow blockages unless systematically analyzed and resolved.

### b) Why is this problem complex?
- [X] **Requires multiple engineering concepts**: Directed Acyclic Graph (DAG) commit trees, tree hashing, 3-way merge algorithms, and working tree state management.
- [X] **Requires analysis and decision making**: Evaluating competing line changes, preserving semantic correctness of both features, and synthesizing a conflict-free resolution.
- [X] **Involves design constraints**: Maintaining commit history integrity, preventing source regression, and enforcing stable branching conventions.
- [X] **Requires use of engineering tools**: Git CLI, GitHub remote cloud hosting, and conflict resolution diff engines.
- [X] **Requires performance/security/safety consideration**: Safeguarding codebase from accidental loss, preventing unauthorized history rewrites, and maintaining clean branch topology.

---

## 4. Knowledge and Tools Required

### Engineering concepts used:
1. Distributed Version Control System (DVCS) Architecture and Directed Acyclic Graph (DAG) commit trees.
2. Git 3-Way Merge Algorithm (common ancestor baseline, HEAD branch state, incoming branch state).
3. Merge Conflict Marker Demarcation Syntax (`<<<<<<< HEAD`, `=======`, `>>>>>>> feature`).
4. Git State Transitions (Working Directory → Staging Index → Local Repository → Remote Repository).

### Tools/Software/Hardware used:
1. Git CLI (Version 2.55.0 on Windows)
2. GitHub (Remote Cloud Repository: `https://github.com/Raghavendra-2007/Git-Branching-and-Merge-Conflict-Resolution`)
3. Operating System / Terminal: Windows PowerShell / Visual Studio Code

---

## 5. Proposed Solution Design

### Architecture / Block Diagram:
```
+------------------------------------------------------------------------------------+
|                               LOCAL REPOSITORY                                     |
|                                                                                    |
|   [Initial Commit: aee5835] (main)                                                 |
|               |                                                                    |
|        +------+------+                                                             |
|        |             |                                                             |
|        v             v                                                             |
|  (main Branch)   (feature Branch)                                                  |
|  Commit: a1a2f4b  Commit: 452eb12                                                  |
|  "Main Website"  "Feature Branch"                                                  |
|        |             |                                                             |
|        +------+------+                                                             |
|               |                                                                    |
|               v                                                                    |
|         [git merge] ----> CONFLICT DETECTED (index.html)                           |
|               |           (<<<<<<< HEAD ... ======= ... >>>>>>> feature)           |
|               v                                                                    |
|      [Manual Resolution]                                                           |
|               |                                                                    |
|               v                                                                    |
|    [Merge Commit: 971f733]                                                         |
|    "Welcome to Main Website - Feature Update"                                      |
+-----------------------+------------------------------------------------------------+
                        |  git push -u origin main
                        |  git push -u origin feature
                        v
+------------------------------------------------------------------------------------+
|                               GITHUB REMOTE                                        |
|   https://github.com/Raghavendra-2007/Git-Branching-and-Merge-Conflict-Resolution  |
|   Branches: main (default, 971f733), feature (452eb12)                             |
+------------------------------------------------------------------------------------+
```

### Brief Working:
The solution initializes a Git repository with `main` as the default branch and creates a baseline commit containing `index.html`. An isolated feature branch `feature` is spawned, simulating an independent developer modifying lines 7–8 to introduce feature content. Concurrently, on the `main` branch, another modification is committed targeting the exact same lines. When `feature` is merged into `main`, Git identifies conflicting line-level modifications and pauses the merge, writing conflict markers into `index.html`. The conflict is manually reconciled by synthesizing the changes into a cohesive HTML structure. The resolved file is staged, a merge commit is recorded, and the complete multi-branch history is synchronized to the remote GitHub repository.

---

## 6. Implementation / Procedure

- **Step 1**: Initialized empty Git repository with `main` as default branch:
  ```powershell
  git init -b main
  git config user.name "Raghava m"
  git config user.email "mylavarapu.kumar132049@marwadiuniversity.ac.in"
  ```
- **Step 2**: Created initial baseline `index.html` with "Welcome to Main Branch" and committed:
  ```powershell
  git add index.html
  git commit -m "Initial commit with index page"  # Commit: aee5835
  ```
- **Step 3**: Created and switched to feature branch:
  ```powershell
  git checkout -b feature
  ```
- **Step 4**: Modified `index.html` on `feature` branch to "Welcome to Feature Branch" and committed:
  ```powershell
  git add index.html
  git commit -m "Update index page in feature branch"  # Commit: 452eb12
  ```
- **Step 5**: Switched back to `main` branch and made conflicting change on the same lines to "Welcome to Main Website":
  ```powershell
  git checkout main
  git add index.html
  git commit -m "Update index page in main branch"  # Commit: a1a2f4b
  ```
- **Step 6**: Merged `feature` into `main`, triggering conflict:
  ```powershell
  git merge feature
  # Output: CONFLICT (content): Merge conflict in index.html
  ```
- **Step 7**: Inspected conflict markers in `index.html` demarcated by `<<<<<<< HEAD`, `=======`, and `>>>>>>> feature`.
- **Step 8**: Manually edited `index.html` to integrate both updates into "Welcome to Main Website - Feature Update".
- **Step 9**: Staged resolved file and completed merge commit:
  ```powershell
  git add index.html
  git commit -m "Resolve merge conflict between main and feature"  # Commit: 971f733
  ```
- **Step 10**: Verified commit DAG history tree:
  ```powershell
  git log --oneline --graph --all
  ```
- **Step 11**: Connected to GitHub remote repository:
  ```powershell
  git remote add origin https://github.com/Raghavendra-2007/Git-Branching-and-Merge-Conflict-Resolution.git
  ```
- **Step 12**: Pushed both branches to remote repository:
  ```powershell
  git push -u origin main
  git push -u origin feature
  ```

---

## 7. Testing and Results

| Test / Parameter | Expected Result | Obtained Result |
| :--- | :--- | :--- |
| **Branch Creation & Isolation** | `feature` branch created independently of `main` | Branch created; independent HEAD pointers maintained |
| **Divergent Line Modifications** | Both branches commit changes to identical line numbers in `index.html` | Distinct commit hashes generated (`452eb12` on feature, `a1a2f4b` on main) |
| **Conflict Detection** | Git halts auto-merge on conflicting lines | `CONFLICT (content): Merge conflict in index.html` received |
| **Conflict Marker Generation** | Markers indicate HEAD vs feature differences | `<<<<<<< HEAD`, `=======`, `>>>>>>> feature` accurately embedded |
| **Manual Resolution** | Clean file created with markers removed and staged | File staged cleanly; merge commit `971f733` generated |
| **Commit History Graph** | Graphical DAG reflects diverging and converging branches | `git log --oneline --graph --all` shows 2-parent merge commit |
| **Remote Synchronization** | Both branches synchronized to GitHub remote | Verified on GitHub: `main` and `feature` branches live |

---

## 8. Challenges Faced and Solutions

| Challenge | Solution |
| :--- | :--- |
| **Automatic 3-way merge failure due to overlapping line edits** | Analyzed conflict markers and manually reconciled both branch features into a unified layout without data loss. |
| **Risk of corrupting working tree during conflict state** | Inspected `git status` at each transition and verified staging area before finalizing the merge commit. |
| **Multi-branch remote synchronization to GitHub** | Configured upstream tracking for both `main` and `feature` using `git push -u origin <branch>`. |

---

## 9. Conclusion
The complex engineering problem of managing concurrent branch modifications and reconciling merge conflicts in distributed version control was successfully solved. By simulating realistic divergent changes across `main` and `feature` branches, the automated failure mechanism was analyzed and corrected through manual conflict resolution. The outcome is a verified, fully merged codebase with preserved commit history published to GitHub (https://github.com/Raghavendra-2007/Git-Branching-and-Merge-Conflict-Resolution). This practical established robust competence in collaborative Git workflows and conflict mitigation.

---

## 10. SDG Mapping and Justification
- **SDG 4 (Quality Education)**: Promotes mastery of modern, industry-standard collaborative engineering practices and version control systems critical for professional software careers.
- **SDG 9 (Industry, Innovation, and Infrastructure)**: Fosters reliable, collaborative software infrastructure through open-source version control and distributed development practices.

---

## 11. References (in IEEE Style)
- [1] S. Chacon and B. Straub, *Pro Git*, 2nd ed. New York, NY, USA: Apress, 2014.
- [2] J. Loeliger and M. McCullough, *Version Control with Git: Powerful tools and techniques for collaborative software development*, 2nd ed. Sebastopol, CA, USA: O'Reilly Media, 2012.
- [3] Git Documentation, "git-merge - Join two or more development histories together," *Git SCM Documentation*, 2026. [Online]. Available: https://git-scm.com/docs/git-merge.
