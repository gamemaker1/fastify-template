# Contributing Guide

Thanks for your interest in contributing to `fastify-template`! This guide will
show you how to set up your environment and contribute to this library.

## Set Up

First, you need to install and be familiar the following:

- `git`: [Here](https://github.com/git-guides) is a great guide by GitHub on
  installing and getting started with Git.
- `node` and `npm`:
  [This guide](https://nodejs.org/en/download/package-manager/) will help you
  install Node and npm. The recommended method is using the `n` version manager
  if you are on MacOS or Linux. Make sure you are using the
  [`current` version](https://github.com/nodejs/Release#release-schedule) of
  Node.

Once you have installed the above, follow
[these instructions](https://docs.github.com/en/get-started/quickstart/fork-a-repo)
to
[`fork`](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks)
and [`clone`](https://github.com/git-guides/git-clone) the repository
(`gamemaker1/fastify-template`).

Once you have forked and cloned the repository, you can
[pick out an issue](https://github.com/gamemaker1/fastify-template/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc)
you want to fix/implement!

## Making Changes

Once you have cloned the repository to your computer (say, in
`~/code/fastify-template`) and picked the issue you want to tackle, create a
branch:

```sh
> git switch --create branch-name
```

While naming your branch, try to follow the below guidelines:

1. Prefix the branch name with the type of change being made:
   - `fix`: For a bug fix.
   - `feat`: For a new feature.
   - `test`: For any change related to tests.
   - `perf`: For a performance related change.
   - `build`: For changes related to the build process.
   - `ci`: For all changes to the CI files.
   - `refc`: For any refactoring work.
   - `docs`: For any documentation related changes.
2. Make the branch name short but self-explanatory.

Once you have created a branch, you can start coding!

The server is written in
[Typescript](https://github.com/microsoft/TypeScript#readme) using the
[Fastify framework](https://github.com/fastify/fastify#readme) and uses the
[`current` version](https://github.com/nodejs/Release#release-schedule) of Node.
The code is structured as follows:

```sh
fastify-template
├── config
│  ├── dev.env.sample
│  ├── prod.env.sample
│  └── test.env.sample
├── patches
│  ├── fastify+4.0.3.patch
│  └── zx+7.0.1.patch
├── scripts
│  ├── utilities
│  │  └── logger.ts
│  ├── clean.ts
│  ├── compile.ts
│  ├── develop.ts
│  ├── start.ts
│  └── test.ts
├── source
│  ├── handlers
│  │  ├── index.ts
│  │  └── templates.ts
│  ├── loaders
│  │  ├── index.ts
│  │  ├── plugins.ts
│  │  ├── routes.ts
│  │  └── schemas.ts
│  ├── provider
│  │  └── database.ts
│  ├── types
│  │  ├── api.d.ts
│  │  ├── database.d.ts
│  │  └── fastify.d.ts
│  ├── utilities
│  │  ├── config.ts
│  │  ├── errors.ts
│  │  ├── logger.ts
│  │  └── misc.ts
│  └── server.ts
├── tests
│  ├── fixtures
│  │  └── ...
│  ├── helpers
│  │  └── fixtures.ts
│  └── integration
│     └── api.ts
├── changelog.md
├── contributing.md
├── package.json
├── pnpm-lock.yaml
├── readme.md
└── tsconfig.json
```

> Most files have a little description of what they do at the top.

#### `./`

- `package.json`: Node package manifest. This file contains the name, version,
  description, dependencies, scripts and package configuration of the project.
- `pnpm-lock.yaml`: PNPM lock file, please do not modify it manually. Run
  `pnpm install` to update it if you add/remove a dependency to/from
  `package.json` manually.
- `tsconfig.json`: The Typescript configuration for this project.
- `changelog.md`: A list of changes that have been made in each version.
- `contributing.md`: The file you are reading. It helps contributors get
  started.
- `license.md`: Tells people how they can use the code.
- `readme.md`: The file everyone should read before running the server. Contains
  installation and usage instructions.

#### `config/`

- `*.env.sample`: An example configuration for each environment, i.e.,
  `development`, `testing` and `production`, that contains variables loaded into
  the environment when the server is running. These environment variables are
  then parsed and exported by `source/utilities/config.ts`. You will need to
  remove the `.sample` file extension and fill in the actual values for all
  variables.
- `*.env`: Do NOT commit these files. EVER. They contain actual sensitive values
  that help the server run.

#### `patches/`

- `*.patch`: These patch files change the code of some libraries we use when
  they don't work as we want them to.

#### `scripts/`

- `clean.ts`: Cleans up all generated files, e.g., `build/`, `coverage/`,
  `*.log`, etc.
- `compile.ts`: Compiles the server to a single `.js` file using `tsup` that can
  be run in production.
- `develop.ts`: Starts the server in development mode and watches the `source/`
  directory for changes. If a file changes, then it reloads the server.
- `start.ts`: Starts the server in production mode (assuming the `compile`
  script has already been run).
- `test.ts`: Runs the Typescript compiler to check types and then `ava` with
  `c8` to run the tests.

#### `source/handlers/`

- `index.ts`: Exports all the handlers from the `handlers/` folder.
- `templates.ts`: The handler for all APIs related to 'templates', e.g.,
  `get /templates` (list), `post /templates` (create), `patch /templates/{id}`
  (update), `get /templates/{id}` (fetch), `delete /templates/{id}` (delete).

#### `source/loaders/`

- `index.ts`: Exports a `build/` function that creates a Fastify application,
  runs all the loaders in the `loaders/` folder, and returns the application.
- `plugins.ts`: Loads all plugins, middleware and the providers from the
  `provider/` folder for the server.
- `routes.ts`: Registers all the handlers from the `handlers/` folder with their
  respective routes.
- `schemas.ts`: Defines the AJV schemas needed for validating requests.

#### `source/providers/`

- `database.ts`: Exports the database service used by the server.

#### `source/types/`

- `api.d.ts`: Type definitions for the interfaces used in the code.
- `database.d.ts`: Type definitions for the Database class that we decorate the
  Fastify instance with.
- `fastify.d.ts`: Type definitions for the decorations we add to the Fastify
  instance.

#### `source/utilities/`

- `utilities/config.ts`: Parses environment variables for configuration.
- `utilities/errors.ts`: Defines and exports a custom error class used to throw
  HTTP errors in handlers.
- `utilities/logger.ts`: Defines and exports a custom logger used in the code.
- `utilities/misc.ts`: Exports utility functions and wrappers around other
  libraries.

#### `source/`

- `server.ts`: Builds the server using the `build()` function from
  `loaders/index.ts` and listens to the port specified in the config.

#### `tests/fixtures/`

- `*`: A set of JSON payloads used to test the server in integration and unit
  tests.

#### `tests/helpers/`

- `fixtures.ts`: Exports a helper function to load fixtures from the `fixtures/`
  folder.

#### `tests/integration/`

- `api.ts`: The API integration test suite.

When adding a new feature/fixing a bug, please add/update the readme and
changelog as well as add tests for the same. Also make sure your code has been
linted and that existing tests pass. You can run the linter using `pnpm lint`,
the tests using `pnpm test` and try to automatically fix most lint issues using
`pnpm format`.

Once you have made changes to the code, you will want to
[`commit`](https://github.com/git-guides/git-commit) (basically, Git's version
of save) the changes. To commit the changes you have made locally:

```sh
> git add this/folder that/file
> git commit --message 'commit-message'
```

While writing the `commit-message`, try to follow the below guidelines:

1. Prefix the message with `type:`, where `type` is one of the following
   dependending on what the commit does:
   - `fix`: Introduces a bug fix.
   - `feat`: Adds a new feature.
   - `test`: Any change related to tests.
   - `perf`: Any performance related change.
   - `build`: For changes related to the build process.
   - `ci`: For all changes to the CI files.
   - `refc`: Any refactoring work.
   - `docs`: Any documentation related changes.
2. Keep the first line brief, and less than 60 characters.
3. Try describing the change in detail in a new paragraph (double newline after
   the first line).

## Contributing Changes

Once you have committed your changes, you will want to
[`push`](https://github.com/git-guides/git-push) (basically, publish your
changes to GitHub) your commits. To push your changes to your fork:

```sh
> git push -u origin branch-name
```

If there are changes made to the `main` branch of the
`gamemaker1/fastify-template` repository, you may wish to
[`rebase`](https://docs.github.com/en/get-started/using-git/about-git-rebase)
your branch to include those changes. To rebase, or include the changes from the
`main` branch of the `gamemaker1/fastify-template` repository:

```
> git fetch upstream main
> git rebase upstream/main
```

This will automatically add the changes from `main` branch of the
`gamemaker1/fastify-template` repository to the current branch. If you encounter
any merge conflicts, follow
[this guide](https://docs.github.com/en/get-started/using-git/resolving-merge-conflicts-after-a-git-rebase)
to resolve them.

Once you have pushed your changes to your fork, follow
[these instructions](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork)
to open a
[`pull request`](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests):

Once you have submitted a pull request, the maintainers of the repository will
review your pull requests. Whenever a maintainer reviews a pull request they may
request changes. These may be small, such as fixing a typo, or may involve
substantive changes. Such requests are intended to be helpful, but at times may
come across as abrupt or unhelpful, especially if they do not include concrete
suggestions on how to change them. Try not to be discouraged. If you feel that a
review is unfair, say so or seek the input of another project contributor. Often
such comments are the result of a reviewer having taken insufficient time to
review and are not ill-intended. Such difficulties can often be resolved with a
bit of patience. That said, reviewers should be expected to provide helpful
feedback.

In order to land, a pull request needs to be reviewed and approved by at least
one maintainer and pass CI. After that, if there are no objections from other
contributors, the pull request can be merged.

#### Congratulations and thanks for your contribution!
