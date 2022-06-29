# <div align="center"> Opiniated Fastify + Typescript Template </div>

<div align="center">
	<img alt="Github Workflow Status" src="https://img.shields.io/github/workflow/status/gamemaker1/fastify-template/CI"/>
	<img alt="GitHub Stars" src="https://img.shields.io/github/stars/gamemaker1/fastify-template"/>
</div>

## What Is This?

An opiniated template for building REST APIs using Fastify and Typescript,
complete with fancy scripts, integration tests and 100% code coverage.

It includes:

- [`fastify`](https://www.fastify.io/) for making your server lightning fast and
  resource efficient.
- [`typescript`](https://www.typescriptlang.org/) +
  [`esm`](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/) for
  writing code (compiles to esm for Node 18).
- [`tsup`](https://tsup.egoist.sh/) +
  [`tsx`](https://github.com/esbuild-kit/tsx#readme) for blazing fast builds.
- [`ava`](https://github.com/avajs/ava#readme) +
  [`c8`](https://github.com/bcoe/c8#readme) for testing and coverage.
- [`xo`](https://github.com/xojs/xo#readme) + [`prettier`](https://prettier.io/)
  for linting and formatting.
- [`pnpm`](https://pnpm.io/) for fast and efficient package management.
- a [contributing guide](./contributing.md), [changelog](./changelog.md),
  [license file](./license.md) and [readme](./readme.md).

## How Do I Use It?

To use this template, `degit` it:

```sh
$ mkdir <project-name>
$ pnpx degit gamemaker1/fastify-template
$ pnpm install
```

Then replace the package name in the manifest (`package.json`), the changelog,
the contributing guide, and the readme (including the badges, if you keep
them!), and get coding :rocket:

## License

You can use this template for any project! The `license.md` file in this
repository IS NOT the license for this template - it is part of the template,
and you can change it as you wish.
