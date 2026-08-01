# SiteMills CLI

SiteMills CLI Tool for project code management on the SiteMills platform.

> [!IMPORTANT]
> **Repository Sync & Release Workflow:**
> This is the internal private source code repository (`sitemills-cli-internal`). The public repository (`sitemills-cli`) contains only the compiled/obfuscated binaries and documentation.
> To prevent code and documentation divergence, you must sync changes to the public repository whenever this repo is updated:
> 
> 1. Commit and push your code updates in this internal repository.
> 2. Compile the obfuscated binaries:
>    ```bash
>    npm install && npm run build
>    ```
> 3. Copy the updated `README.md` and the new binaries from `dist/binaries/` to the public `sitemills-cli` repository.
> 4. Commit and push the updates in the public repository to release them to users.

## Installation

### From Source

Clone the repository and install dependencies (none required, uses Node.js standard library):

```bash
git clone <repository-url> sitemills-cli
cd sitemills-cli
```

To install the command globally during development:

```bash
npm link
```

This will register the `sitemills-cli` command globally on your system.

## Usage

```bash
sitemills-cli <command> [options]
```

### Available Commands

- **login**: Authenticate with the SiteMills host.
  ```bash
  sitemills-cli login
  ```
- **list**: List all projects.
  ```bash
  sitemills-cli list
  ```
- **credits**: Query and check remaining credit and token usage balances for a project.
  ```bash
  sitemills-cli credits <projectId>
  ```
- **storage**: Retrieve a detailed storage usage breakdown (database, media uploads, branches, versions, etc.).
  ```bash
  sitemills-cli storage <projectId>
  ```
- **billing-history**: View transaction and order history for your account or project.
  ```bash
  sitemills-cli billing-history [projectId] [--limit <limit>]
  ```
- **import**: Import a local project directory into a new SiteMills project.
  ```bash
  sitemills-cli import <projectName> <inputDir>
  ```
- **seed**: Seed a local folder from a SiteMills project template.
  ```bash
  sitemills-cli seed <projectName> [outputDir] [--type <structureType>]
  ```
- **seed-db**: Seed database records for a project/branch from a JSON file.
  ```bash
  sitemills-cli seed-db <projectId> <branchId> <dataFile.json>
  ```
- **export**: Export project code from a branch to a local directory.
  ```bash
  sitemills-cli export <projectId> [branchId] <outputDir>
  ```
- **push**: Push local updates/commits to a specific branch on SiteMills.
  ```bash
  sitemills-cli push <projectId> <branchId> <inputDir> [--message <message>]
  ```
- **deploy**: Deploy a branch to an environment (DEV, STAGING, or PROD).
  ```bash
  sitemills-cli deploy <projectId> <branchId> <environment>
  ```
- **compile**: Trigger manual project code compilation for a branch and check results.
  ```bash
  sitemills-cli compile <projectId> [--branch <branchId>]
  ```
- **logs**: Fetch and view the project's execution and runtime logs, with optional branch, environment, and level filtering.
  ```bash
  sitemills-cli logs <projectId> [--branch <branchId>] [--env <environment>] [--level <level>] [--limit <limit>]
  ```
- **workflows**: List recent agentic/AI workflows run on the project, including their status, prompt, and execution token costs.
  ```bash
  sitemills-cli workflows <projectId> [--branch <branchId>] [--limit <limit>]
  ```
- **set-visibility**: Change project visibility to PRIVATE, UNLISTED, or PUBLIC, with optional SEO indexing enablement.
  ```bash
  sitemills-cli set-visibility <projectId> <visibility> [--indexable | --no-indexable]
  ```
- **delete**: Delete a project on SiteMills.
  ```bash
  sitemills-cli delete <projectId>
  ```
- **data-op**: Execute a data operation payload.
  ```bash
  sitemills-cli data-op <projectId> <payloadJsonOrFile> [--branch <branchId>] [--env <environment>]
  ```
- **run-lua**: Execute a Lua script against a collection.
  ```bash
  sitemills-cli run-lua <projectId> <collection> <luaScriptFile> [--branch <branchId>] [--env <environment>] [--filter <jsonFilter>] [--dry-run]
  ```
- **list-branches**: List all development branches for a project, including their kind (e.g. WORKING or CHECKPOINT), active deployed environments, and version references.
  ```bash
  sitemills-cli list-branches <projectId>
  ```
- **members**: List project team members, roles, and pending invitation status.
  ```bash
  sitemills-cli members <projectId>
  ```
- **invite**: Invite a new collaborator to the project with OWNER, DEVELOPER, or READER privileges.
  ```bash
  sitemills-cli invite <projectId> <email> <role>
  ```
- **remove-member**: Remove a team member or revoke a pending invitation by ID or email.
  ```bash
  sitemills-cli remove-member <projectId> <emailOrId>
  ```
- **version-history**: View the timeline of code versions and checkpoints for a specific branch.
  ```bash
  sitemills-cli version-history <projectId> [branchId] [--limit <limit>]
  ```
- **list-tasks**: List all planning and execution tasks on the project task board.
  ```bash
  sitemills-cli list-tasks <projectId>
  ```
- **add-task**: Add a new task to the project's task board.
  ```bash
  sitemills-cli add-task <projectId> <title> [description] [--priority <N>] [--assignee <email>]
  ```
- **update-task**: Update an existing task's title, description, priority, assignee, or status.
  ```bash
  sitemills-cli update-task <projectId> <taskId> [--title <title>] [--description <desc>] [--priority <N>] [--assignee <email>] [--status <status>]
  ```
- **env-list**: List all resolved environment variables for a project environment.
  ```bash
  sitemills-cli env-list <projectId> <environment>
  ```
- **env-set**: Create or update an environment variable/secret.
  ```bash
  sitemills-cli env-set <projectId> <environment> <name> <value> [--description <desc>]
  ```
- **env-delete**: Remove an environment variable/secret from a project environment.
  ```bash
  sitemills-cli env-delete <projectId> <environment> <name>
  ```
- **payments-status**: Fetch the Stripe Connect payouts and configuration status.
  ```bash
  sitemills-cli payments-status <projectId> <siteEnvironment>
  ```
- **setup-payments**: Interactively guide Stripe Connect payouts onboarding for an environment/scope.
  ```bash
  sitemills-cli setup-payments <projectId> <siteEnvironment> [--owner-name <ownerName>] [--country <country>]
  ```
- **upload-media**: Upload a local media file to SiteMills storage.
  ```bash
  sitemills-cli upload-media <projectId> <filePath> [--type <uploadType>]
  ```
- **set-branding**: Configure project branding assets (banner, gallery, video) using media IDs.
  ```bash
  sitemills-cli set-branding <projectId> --banner <bannerMediaId> [--gallery <mediaId1,mediaId2>] [--video <showcaseVideoMediaId>]
  ```
- **set-description**: Update the public display description of the project.
  ```bash
  sitemills-cli set-description <projectId> <description>
  ```
- **encryption**: Manage project data encryption at rest (status check, secure key generation, configuring key, enabling encryption).
  ```bash
  sitemills-cli encryption <projectId> [status | generate-key | set-key <key> | enable]
  ```

### Options

- `--message <msg>`: Commit message for push (default: `CLI push update`)
- `--branch <branch>`: Target branch ID
- `--env <environment>`: Target environment name (`DEV`, `STAGING`, or `PROD`)
- `--filter <filter>`: JSON query filter for `run-lua`
- `--dry-run`: Execute Lua script as a dry run
- `--limit <limit>`: Max documents matched for `run-lua`
- `--max-write-ops <N>`: Max writes allowed for `run-lua`
- `--type <type>`: Project structure type (`DIRECT` or `CONTRACT_BASED`)
- `--owner-name <name>`: Owner's name to register during Stripe Connect onboarding
- `--country <country>`: Business country code to register during Stripe Connect onboarding (default: `US`)
- `--description <desc>`: Brief description metadata for environment variables
- `--banner <id>`: Media ID of the project banner image
- `--gallery <ids>`: Comma-separated media IDs to add to the project gallery
- `--video <id>`: Media ID of the project showcase video
