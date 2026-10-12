# **LAB 2 TASK - Maven-Git**

## **Maven Project Creation, Git Version Control, and Branch Management**

**Course:** Computer Programming III

**Lab:** 2

**Total Points:** 100

**Deadline:** Monday, October 12, 2026, at 19:20 

## **Objective**

The objective of this laboratory assignment is to practice creating and running a Java Maven project, configuring `.gitignore`, initializing a Git repository from a downloaded ZIP template, managing the staging area, connecting to GitHub, and working with multiple branches.

## **Required Tools**

- Java JDK
- Apache Maven
- Git
- GitHub account
- Windows PowerShell

## **General Instructions**

- Use your **assigned GitHub repository** throughout the task.
- Replace example names and URLs with your own GitHub information.
- Run Git commands from the **root directory of the extracted GitHub template**, unless a step says otherwise.

---

## **Task 1 — Download and Extract the GitHub Template (10 Points)**

**Step 1.** Log in to your GitHub account and open your assigned repository (`lab-02-GitHubUsername`).

**Step 2.** Click **Code → Download ZIP** to download the repository as a ZIP file.

**Step 3.** Extract the downloaded ZIP file to your Desktop.

**Step 4.** Open Windows PowerShell and navigate to the extracted repository directory:


```powershell
cd Desktop
cd lab-02-USERNAME-main
```

Replace `USERNAME` with your GitHub username, and use the actual name of your extracted folder if it is different.

**Step 5.** Verify that you are in the correct directory:

```powershell
pwd
```

**Important:** A ZIP download contains the project files but does **not** include the Git history or the `.git` directory. You will initialize Git in Task 4.

---

## **Task 2 — Maven Project Creation, Compilation, and Execution (20 Points)**

**Step 1.** Create a new Java Maven project in the extracted repository directory using Maven Archetype. Enter the command on a single line:

```powershell
mvn -B archetype:generate "-DgroupId=com.example" "-DartifactId=Lab2-task" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DarchetypeVersion=1.5"
```

**Step 2.** Navigate to the generated Maven project directory:

```powershell
cd Lab2-task
```

**Step 3.** Compile and package the Maven project:

```powershell
mvn clean package
```

Verify that the build completes successfully. Expected output includes:

```text
[INFO] BUILD SUCCESS
```

**Step 4.** Run the compiled Java application:

```powershell
java -cp target/Lab2-task-1.0-SNAPSHOT.jar com.example.App
```

Expected program output:

```text
Hello World!
```

**Important:** Do not delete the generated `target/` directory. It is required to observe Git ignore behavior in Task 4.

---

## **Task 3 — Create and Configure the .gitignore File (10 Points)**

**Step 1.** Return to the root directory of the extracted GitHub repository:

```powershell
cd ..
```

**Step 2.** Create a file named **`.gitignore`** in the repository root, **outside** the `Lab2-task/` folder.

**Step 3.** Open `.gitignore` in a text editor and add the following content:

```gitignore
# Maven build outputs
target/
*.class

# IntelliJ IDEA
.idea/

# VS Code
.vscode/

# Log files
*.log
```

**Step 4.** Save the file. Verify that the folder layout is similar to:

```text
lab-02-USERNAME-main/
├── .gitignore
├── README.md
└── Lab2-task/
    ├── .mvn/
    ├── src/
    ├── pom.xml
    └── target/
```

**Important:** The `target/` rule applies to `target` directories inside the repository, including `Lab2-task/target/`. Keep `target/` on your computer; it should not be included in the Git repository.

---

## **Task 4 — Git Initialization, Staging Area, and Remote Configuration (20 Points)**

**Step 1.** Initialize a local Git repository in the extracted GitHub template root:

```powershell
git init
```

**Step 2.** Attempt to add the generated Maven JAR file to the staging area:

```powershell
git add Lab2-task/target/Lab2-task-1.0-SNAPSHOT.jar
```

**Step 3.** Inspect the repository status:

```powershell
git status
```

Observe why the JAR file was not staged: the `.gitignore` file contains the `target/` rule. An ignored-path warning is expected. Do **not** use `git add -f`.

**Step 4.** Add all non-ignored project files to the staging area:

```powershell
git add .
```

**Step 5.** Examine the staged changes:

```powershell
git diff --staged
```

Verify that the Maven source files, `pom.xml`, `.gitignore`, and `README.md` are staged, but `Lab2-task/target/` is not. If Git displays the output in a pager, press `q` to return to PowerShell.

**Step 6.** Check the staging status and inspect the local branches:

```powershell
git status
git branch
```

**Note:** `git branch` may not display a branch yet because there is no commit.

**Step 7.** Set the local branch name to `main`:

```powershell
git branch -M main
```

**Step 8.** Register your **assigned** GitHub repository as `origin`:

```powershell
git remote add origin https://github.com/CENG-ES/lab-02-USERNAME.git
```

**Replace `USERNAME` with your GitHub username.** If your assigned repository has a different URL, use its exact HTTPS URL. Do not create or push to a different repository.

**Step 9.** Verify the remote repository configuration:

```powershell
git remote -v
```

Check that both the `fetch` and `push` URLs point to your assigned GitHub repository.

---

## **Task 5 — Commit, Push, and Branch Management (25 Points)**

**Step 1.** Create the first commit containing the staged project files:

```powershell
git commit -m "Initial project"
```

**Step 2.** Push `main` to the assigned GitHub repository:

```powershell
git push -u origin main
```

**If Git reports `fetch first`:** The downloaded ZIP does not contain the original Git commit history, while your assigned GitHub repository may already contain commits. To integrate two independent histories, use:

```powershell
git pull origin main --allow-unrelated-histories
```

If a commit-message editor (such as Vim) opens, you can accept the default merge message by pressing `Esc`, typing `:wq`, and pressing `Enter`. If Git reports a merge conflict, resolve the affected files and complete the merge before continuing. Then retry:

```powershell
git push -u origin main
```


**Step 3.** Stop tracking `README.md` without deleting the file from your computer:

```powershell
git rm --cached README.md
```

**Step 4.** Commit the removal from Git tracking:

```powershell
git commit -m "Update README"
```

**Step 5.** Create and switch to a new branch named `readme-update`:

```powershell
git switch -c readme-update
```

**Step 6.** Push the new branch to GitHub:

```powershell
git push -u origin readme-update
```

**Important:** Do not push the `README.md` removal commit to the GitHub `main` branch. Do not merge `readme-update` into `main`. The local `README.md` file remains on your computer; it may appear as untracked because it was removed from Git tracking but was not added to `.gitignore`.

---

## **Task 6 — GitHub Repository Verification (15 Points)**

**Step 1.** Open your assigned GitHub repository in a web browser.

**Step 2.** Select the `main` branch and confirm that it matches the provided reference image. The expected structure is:

```text
├── Lab2-task/
│   ├── .mvn/
│   │   ├── jvm.config
│   │   └── maven.config
│   ├── src/
│   │   ├── main/java/com/example/
│   │   └── test/java/com/example/
│   └── pom.xml
├── .gitignore
└── README.md
```

**Step 3.** Use the GitHub branch selector to switch to `readme-update`. Confirm that it has the same Maven project files and `.gitignore` but **does not contain `README.md`**.

**Step 4.** Compare the branches:

| File or Directory | `main` | `readme-update` |
|:--|:--:|:--:|
| `Lab2-task/` | Present | Present |
| `Lab2-task/.mvn/` | Present | Present |
| `Lab2-task/src/` | Present | Present |
| `Lab2-task/pom.xml` | Present | Present |
| `.gitignore` | Present | Present |
| `README.md` | **Present** | **Absent** |
| `Lab2-task/target/` | Absent | Absent |

**Step 5.** Take screenshots of the file listings on **both** GitHub branches as evidence.

**Expected result:** The `main` branch contains `README.md`; the `readme-update` branch does not. Both branches contain the Maven source project and exclude `target/`.

---

## **Submission Requirements**

Submit or provide the following as instructed by your lab instructor:

1. **Assigned GitHub repository URL** (with both branches pushed).
2. **`main` branch screenshot** showing `README.md` and the Maven project files.
3. **`readme-update` branch screenshot** showing that `README.md` is absent.
4. **Maven build screenshot** displaying `BUILD SUCCESS` and evidence of the `Hello World!` program output.
5. **Git staging screenshot** or console output showing that the `target/` JAR file was ignored and the source files were staged.

## **Grading Rubric**

| Task | Points |
|:--|--:|
| Task 1 — Download and Extract Template | 10 |
| Task 2 — Maven Creation and Execution | 20 |
| Task 3 — `.gitignore` Configuration | 10 |
| Task 4 — Git Initialization and Staging | 20 |
| Task 5 — Commit, Push, and Branches | 25 |
| Task 6 — GitHub Verification | 15 |
| **Total** | **100** |

---

## **Important Note — GitHub Authentication Issues (Optional)**

If you encounter an **authentication error** when running `git push`, first use the browser sign-in option if Git offers one. If credential-based authentication is required, you can use a **GitHub Personal Access Token (PAT)** instead of your GitHub account password.

### Step 1 — Generate a Personal Access Token

1. Sign in to your GitHub account.
2. Open **Settings → Developer settings → Personal access tokens → Fine-grained tokens**.
3. Select **Generate new token**.
4. Configure the token:

   - **Token name:** `Lab2-Git`
   - **Expiration:** Choose an appropriate expiration date.
   - **Resource owner:** Select the owner of your assigned repository, if available.
   - **Repository access:** Select your assigned repository.
   - **Repository permissions → Contents:** `Read and write`.
5. Generate the token and copy it to a secure location.

### Step 2 — Authenticate

Retry the relevant command, for example:

```powershell
git push -u origin main
```

If Git asks for credentials, enter your **GitHub username** as the username and paste the **token** as the password. If a browser sign-in window appears, you may authenticate through your browser instead.

**Security and access notes:**

- Never share your token or commit it to GitHub.
- Do not include a token in screenshots, source code, or repository URLs.
- Creating a token does **not** grant repository access if you have not already been authorized.
- Organization-owned repositories may require token approval or may not support your type of fine-grained token access. Ask the course instructors if authentication still fails.
- If `git push` already works, **you do not need to create a token**.

Official documentation: [GitHub — Managing your personal access tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).

---

**Final reminder:** Your submitted GitHub repository must contain both `main` and `readme-update`. The only required file-listing difference between these branches is the absence of `README.md` in `readme-update`.

## **Submission Instructions**

- Submit a **single PDF file via ESTUOYS** ([https://estuoys.eskisehir.edu.tr/](https://estuoys.eskisehir.edu.tr/)) containing your full name, student ID, **terminal commands, and outputs (including errors)**. (`BIM2005_Lab2_YourName_StudentID.pdf`)
- Your code and task completion will be **evaluated through GitHub**.
- **Important:** If either your **GitHub submission** or your **PDF submission** via ESTUOYS  is missing, your work will not be evaluated.

## **Contact Information**

For questions or technical issues related to Lab 2, please contact:

- **Lab Assistant:** Soner ALTUN  
  **Email:** [saltun@eskisehir.edu.tr](mailto:saltun@eskisehir.edu.tr)

- **Lab Assistant:** Ali Emre KÜÇÜKKURT  
  **Email:** [aliemrekucukkurt@eskisehir.edu.tr](mailto:aliemrekucukkurt@eskisehir.edu.tr)
