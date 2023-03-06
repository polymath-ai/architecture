# Monorepo for Node

For the Node environment, we use the monorepo setup, using Node's built-in
[workspace](https://docs.npmjs.com/cli/v9/using-npm/workspaces?v=true) capability.

A lot of this is inspired by the Turbo [monorepo handbook](https://turbo.build/repo/docs/handbook).

## Name of the repository

The name of the repository is `polymath-ai`. It mirrors the name of the organization, and also the name of the `npm` scope.

## The layout

The layout of the repository is as follows:

```text

├── package.json (monorepo configuration)
├── packages
│   ├── <package>
│   │   ├── package.json (each package has its own config)
│   │   └── src
│   │       └── index.js
...

```

In the monorepo configuration `package.json` file, we define the `workspaces` as follows:

```json
{
  "workspaces": ["./packages/*"]
}
```

Each package must have a name that starts with `@polymath-ai/` to signify its scope. For example:

```json

{
  "name": "@polymath-ai/schemas",
  "version": "1.0.0",
  "description": "Contains all configuration schemas for Polymath",
  "main": "src/index.js",
  ...
}

```

## Managing packages within the monorepo

To add a new package, run:

```bash
npm init --scope=@polymath-ai -y -w ./packages/${package}
```

To add one package in the monorepo as a dependency on another, run:

```bash
npm install @polymath-ai/${dependency} -w ./packages/${package}
```

where `${dependency}` is the name of the package to be added as a dependency, and `${package}` is the name of the package that will have the dependency added.

All packages within the monorepo have a similar structure:

```text

├── package.json
├── src
│   ├── index.js
│   ├── index.test.js
│   ├── <dir>
│   │   ├── <file>.js

```

We try to place most of the code into sub-directories of the `src` directory, organizing them according to their purpose.

## Testing

We use [ava](https://github.com/avajs/ava) for testing and place test files next to the source files they test, with the `.test.js` extension.

## Publishing packages

To publish packages, we use [changesets](https://github.com/changesets/changesets). The publishing workflow is:

1. Run `changeset` to create a new changeset. This will prompt you to select the packages that have changed, and will create a new changeset file in the `.changeset` directory.

2. Run `changeset version` to bump the version numbers of the packages that have changed. This will update the `package.json` files of the packages that have changed, and will create a new commit with the changes.

3. Run `changeset publish` to publish the packages that have changed. This will create a new tag for the new version, and will publish the packages to the npm registry.
