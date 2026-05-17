## Development workflow

### 1. Install Tools

#### Task

Common development processes are run using [the **Task** task runner tool](https://taskfile.dev/).

Follow the installation instructions here:<br />
https://taskfile.dev/installation/

#### Node.js

[**npm**](https://www.npmjs.com/) is used for dependency management.

Follow the installation instructions here:<br />
https://nodejs.dev/en/download

Node.js 20.x is used for development of this project. [nvm](https://github.com/nvm-sh/nvm) is recommended to easily switch between Node.js versions.

#### Extras

Some optional tools used by this project:

- [**Python**](https://www.python.org/downloads/)
- [**Poetry**](https://python-poetry.org/docs/#installation)

### 2. Coding

Now you're ready to work some [TypeScript](https://www.typescriptlang.org/) magic!

Make sure to write or update tests for your work when appropriate.

### 3. Format code

Format the code to follow the standard style for the project:

```
npm run format
```

### 4. Run tests

Run the tests to ensure that the code works as expected:

```
task check
```

### 5. Build

It is necessary to compile the code before it can be used by GitHub Actions. Remember to run this command before committing any code changes:

```
task build
```

### 6. Commit

Everything is now ready to make your contribution to the project, so commit it to the repository and submit a pull request.

Thanks!

## Dependency license metadata

Metadata about the license types of all dependencies is cached in the repository. To update this cache, run the following command from the repository root folder:

```
task general:cache-dep-licenses
```

The necessary **Licensed** tool can be installed by following [these instructions](https://github.com/github/licensed#as-an-executable).

Unfortunately, **Licensed** does not have support for being used on the **Windows** operating system.

An updated cache is also generated whenever the cache is found to be outdated by the by the "Check Go Dependencies" CI workflow and made available for download via the `dep-licenses-cache` [workflow artifact](https://docs.github.com/actions/managing-workflow-runs/downloading-workflow-artifacts).

## Enable verbose logging for a pipeline

Additional log events with the prefix ::debug:: can be enabled by setting the secret `ACTIONS_STEP_DEBUG` to `true`.

See [step-debug-logs](https://github.com/actions/toolkit/blob/master/docs/action-debugging.md#step-debug-logs) for reference.

## Release workflow

To release a new version, run:

```
task release VERSION=X.Y.Z
```

This will:

1. Promote the `Unreleased` section of `CHANGELOG.md` to `vX.Y.Z`.
1. Commit, tag (`vX.Y.Z`), and force-update the major version tag (`vX`).
1. Push the commit and both tags to `origin`.

Before running, make sure to:

- Update the action refs in `README.md` examples if incrementing major (e.g., `uses: go-task/setup-task@v1` -> `uses: go-task/setup-task@v2`).
- Run `task check` and `task build` to ensure `dist/` is up to date.
- Follow [the SemVer specification](https://semver.org/).

After the tag is pushed, create the [GitHub release](https://docs.github.com/en/github/administering-a-repository/managing-releases-in-a-repository#creating-a-release) from the `vX.Y.Z` tag, copying the relevant section from `CHANGELOG.md` into the release notes.
