git clone <repository-url>
    cd gym-schedule-management
    ```
2.  **Ensure Gitflow is installed**:
    If not already installed, follow the instructions for your OS:
    *   **Debian/Ubuntu**: `sudo apt-get install git-flow`
    *   **macOS**: `brew install git-flow`
    *   **Windows**: Install Git for Windows and select Gitflow option during installation.
3.  **Initialize Gitflow (if not already done)**:
    ```bash
    git flow init -d
    ```
    This command will set up `main` as the production branch and `develop` as the development branch, creating `develop` if it doesn't exist.

### 2. Feature Development

*   **Start a new feature**: All new features must be developed in a dedicated `feature` branch.
    ```bash
    git flow feature start <feature-name>
    ```
    (e.g., `git flow feature start implement-trainer-dashboard`)
    This command creates a new branch `feature/<feature-name>` off `develop` and switches to it.

*   **Develop your feature**: Write code, commit frequently, and push your branch regularly to the remote.

*   **Commit Messages**: Use **Conventional Commits** for clear and consistent commit history.
    *   **Format**: `<type>(<scope>): <description>`
    *   **Types**: `feat` (new feature), `fix` (bug fix), `docs` (documentation), `style` (formatting, no code change), `refactor` (code change that neither fixes a bug nor adds a feature), `test` (adding missing tests or correcting existing tests), `chore` (maintenance tasks, build process, auxiliary tools, libraries, etc).
    *   **Example**: `feat(booking): implement user booking functionality`
    *   **Example with scope**: `fix(auth): resolve login redirect issue`

*   **Avoid Unnecessary Files**:
    *   **DO NOT** commit temporary files, IDE configuration files (e.g., `.idea/`, `.vscode/`), compiled output (`build/`, `dist/`), log files, or personal environment settings.
    *   Ensure your `.gitignore` file is up-to-date to automatically exclude these types of files.
    *   If you find unnecessary files in the repository, please open an issue or create a pull request to update `.gitignore` and remove them.

*   **Finish a feature**: Once your feature is complete and thoroughly tested, merge it back into `develop`.
    ```bash
    git flow feature finish <feature-name>
    ```
    This command merges `feature/<feature-name>` into `develop`, deletes the `feature` branch, and switches back to `develop`.
    *   **Important**: Before finishing, ensure your `develop` branch is up-to-date. It's recommended to `git pull origin develop` and then rebase your feature branch on the latest `develop` before finishing to resolve conflicts cleanly.

*   **Pull Requests**: After `git flow feature finish`, push your updated `develop` branch to the remote. If you are working in a team environment or need code review, create a Pull Request from your `feature` branch to `develop` *before* finishing the feature locally. The `git flow feature finish` command can then be run after the PR is merged.

### 3. Release Management

*   **Start a release**: When `develop` is stable enough for a new release.
    ```bash
    git flow release start <version-number>
    ```
    (e.g., `git flow release start 1.0.0`)
    This creates `release/<version-number>` off `develop`.

*   **Prepare for release**: Perform final bug fixes, documentation updates, and version bumping on the `release` branch.

*   **Finish a release**: Once the release is ready, merge it.
    ```bash
    git flow release finish <version-number>
    ```
    This merges `release/<version-number>` into `main` and `develop`, tags `main` with the version number, and deletes the `release` branch. Immediately push the `main` and `develop` branches and the new tag to the remote repository.

### 4. Hotfixes

*   **Start a hotfix**: For critical bugs in `main` that need immediate attention.
    ```bash
    git flow hotfix start <description>
    ```
    (e.g., `git flow hotfix start critical-login-bug`)
    This creates `hotfix/<description>` off `main`.

*   **Apply fix**: Implement the necessary bug fix.

*   **Finish a hotfix**:
    ```bash
    git flow hotfix finish <description>
    ```
    This merges `hotfix/<description>` into `main` and `develop`, tags `main` with the hotfix version, and deletes the `hotfix` branch. Immediately push the `main` and `develop` branches and the new tag to the remote repository.

### 5. Code Review and Testing

*   All code changes are subject to review.
*   Ensure all new features or bug fixes have corresponding tests (unit, integration, E2E) where applicable.
*   All existing tests must pass before submitting a pull request or finishing a feature/release/hotfix.

## Development Environment Setup

To get a local copy up and running, follow these simple steps.

### Prerequisites

*   Node.js (LTS version recommended)
*   npm (usually comes with Node.js)
*   Git

### Installation

1.  **Clone the repository**:
    ```bash
    git clone <repository-url>
    cd gym-schedule-management
    ```
2.  **Install dependencies**:
    ```bash
    npm install
    ```
3.  **Configure environment variables**:
    Create a `.env` file in the root directory. Consult `sample.env` (if provided) for required variables, or refer to project documentation for environment configuration.

### Running the Project

To start the development server: