# Build and Test Node.js with GitHub Actions

## Overview

GitHub Actions provides Runners with Linux, Windows, or Apple OSes, and supports installing dependencies and executing shell commands to build, test, and deploy node.js apps.

## Runners

GitHub provides 'Runners' that are pre-defined environments used for build, test, and deploy operations.

Runners come with specific minimum capabilities like:

- Yarn.
- npm.

Windows-based runners _also_ have:

- Grunt.
- Gulp.
- Bower.

Runners can cache dependencies to speed up builds.

### Installing Dependencies

- Just like on your local machine, use `npm i` to install dependencies.
- Package.json must be up-to-date and functionally correct.
- After you install dependencies, other apps and shell commands can be available!
- `package-lock.json` and `npm-shrinkwrap.json` are supported.

Commands:

- `npm i`: The usual too.
- `npm ci`: Tends to be [faster](https://blog.npmjs.org/post/171556855892/introducing-npm-ci-for-faster-more-reliable).

_Note_: Private registry installation using `.npmrc` file is supported. Use `setup-node` action to support this feature (required tokens/encrypted secrets).

## Workflows

- Use YAML to define the workflow.
- Store in `.github/workflows` folder in your repository.
- `on`: Defines the Git event that triggers the workflow.
- `jobs`: Defines the work to perform.
- `build`: Name of the job.
- `runs-on`: Defines the OS to run the job on.
- `strategy`: Defines the matrix of Node.js versions to run the job on.
- `steps`: Defines the steps to run in the job.
- `uses`: Defines the GitHub action to run.
- `with`: Defines the parameters to pass to the action.
- `run`: Defines the shell commands to run.

## GitHub Actions

- There are GitHub repositories of Actions that can be used.
- Reference them like `uses: actions/setup-node@v3`.
- There are Action predefined for many OSes, build environments, etc.

## With

Parameters might include:

- matrix.node-version: References a collection Node.js version to use.
- matrix.os: References a collection of OSes to use.
- Written like: `${{ matrix.node-version }}`.
- See `strategy: matrix: node-version: [...]` for the collection of Node.js versions to use.
- Same for OSes.

## Run

Defines the shell command to run:

- If you want to execute npm build (a shell command) then do: `npm run build`.
- Other commands are available including OS-build-in commands.
- OS must have the command available.

## Node-Version

- Collection: `with: node-version: [...]`.
- Single (major) version: `with: node-version: 16.x`.
- Exact version: `with: node-version: 16.2.3`.

## Workflow Artifact Storage

See GitHub Docs [Storing workflow data as artifacts](https://docs.github.com/en/actions/guides/storing-workflow-data-as-artifacts).

## Pushing to Package Registries

See GitHub Docs [Publishing Node.js packages](https://docs.github.com/en/actions/guides/publishing-nodejs-packages).

## References

- [Build and Test Node.js with GitHub Actions](https://docs.github.com/en/actions/guides/building-and-testing-nodejs)
- NPM Blog [IOntroducing npm ci for faster, more reliable builds](https://blog.npmjs.org/post/171556855892/introducing-npm-ci-for-faster-more-reliable).

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
