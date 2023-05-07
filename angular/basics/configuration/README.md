# Configuration

## Workspace

A workspace contains the files for one or more projects. A project is the set of files that comprise a standalone application or a shareable library.  By default, `ng new` creates an initial skeleton application at the root level of the workspace, along with its end-to-end tests. The skeleton is for a simple Welcome application that is ready to run and easy to modify. The root-level application has the same name as the workspace, and the source files reside in the `src/` subfolder of the workspace.

### Workspace configuration files <a href="#workspace-configuration-files" id="workspace-configuration-files"></a>

| WORKSPACE CONFIG FILES | PURPOSE                                                                                                                                                                                                                                                                                                                                                                                            |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `.editorconfig`        | Configuration for code editors. See [EditorConfig](https://editorconfig.org/).                                                                                                                                                                                                                                                                                                                     |
| `.gitignore`           | Specifies intentionally untracked files that [Git](https://git-scm.com/) should ignore.                                                                                                                                                                                                                                                                                                            |
| `README.md`            | Introductory documentation for the root app.                                                                                                                                                                                                                                                                                                                                                       |
| `angular.json`         | CLI configuration defaults for all projects in the workspace, including configuration options for build, serve, and test tools that the CLI uses, such as [TSLint](https://palantir.github.io/tslint/), [Karma](https://karma-runner.github.io/), and [Protractor](http://www.protractortest.org/). For details, see [Angular Workspace Configuration](https://angular.io/guide/workspace-config). |
| `package.json`         | Configures [npm package dependencies](https://angular.io/guide/npm-packages) that are available to all projects in the workspace. See [npm documentation](https://docs.npmjs.com/files/package.json) for the specific format and contents of this file.                                                                                                                                            |
| `package-lock.json`    | Provides version information for all packages installed into `node_modules` by the npm client. See [npm documentation](https://docs.npmjs.com/files/package-lock.json) for details. If you use the yarn client, this file will be [yarn.lock](https://yarnpkg.com/lang/en/docs/yarn-lock/) instead.                                                                                                |
| `src/`                 | Source files for the root-level application project.                                                                                                                                                                                                                                                                                                                                               |
| `node_modules/`        | Provides [npm packages](https://angular.io/guide/npm-packages) to the entire workspace. Workspace-wide `node_modules` dependencies are visible to all projects.                                                                                                                                                                                                                                    |
| `tsconfig.json`        | The `tsconfig.json` file is a ["Solution Style"](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-9.html#support-for-solution-style-tsconfigjson-files) TypeScript configuration file. Code editors and TypeScript’s language server use this file to improve development experience. Compilers do not use this file.                                                       |
| `tsconfig.base.json`   | The base [TypeScript](https://www.typescriptlang.org/) configuration for projects in the workspace. All other configuration files inherit from this base file. For more information, see the [Configuration inheritance with extends](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html#configuration-inheritance-with-extends) section of the TypeScript documentation.             |
| `tslint.json`          | Default [TSLint](https://palantir.github.io/tslint/) configuration for projects in the workspace.                                                                                                                                                                                                                                                                                                  |

### Application configuration files

&#x20;For a multi-project workspace, project-specific configuration files are in the project root, under `projects/project-name/`.

| APPLICATION-SPECIFIC CONFIG FILES | PURPOSE                                                                                                                                                                                                                                                                                                            |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `.browserslistrc`                 | Configures sharing of target browsers and Node.js versions among various front-end tools. See [Browserslist on GitHub](https://github.com/browserslist/browserslist) for more information.                                                                                                                         |
| `karma.conf.js`                   | Application-specific [Karma](https://karma-runner.github.io/2.0/config/configuration-file.html) configuration.                                                                                                                                                                                                     |
| `tsconfig.app.json`               | Application-specific [TypeScript](https://www.typescriptlang.org/) configuration, including TypeScript and Angular template compiler options. See [TypeScript Configuration](https://angular.io/guide/typescript-configuration) and [Angular Compiler Options](https://angular.io/guide/angular-compiler-options). |
| `tsconfig.spec.json`              | [TypeScript](https://www.typescriptlang.org/) configuration for the application tests. See [TypeScript Configuration](https://angular.io/guide/typescript-configuration).                                                                                                                                          |
| `tslint.json`                     | Application-specific [TSLint](https://palantir.github.io/tslint/) configuration.                                                                                                                                                                                                                                   |

## Multiple projects

A multi-project workspace is suitable for an enterprise that uses a single repository and global configuration for all Angular projects (the "monorepo" model). A multi-project workspace also supports library development.

```
my-workspace/
  ...             (workspace-wide config files)
  projects/       (generated applications and libraries)
    my-first-app/ --(an explicitly generated application)
      ...         --(application-specific config)
      e2e/        ----(corresponding e2e tests)
         src/     ----(e2e tests source)
         ...      ----(e2e-specific config)
      src/        --(source and support files for application)
    my-lib/       --(a generated library)
      ...         --(library-specific config)
      src/        --source and support files for library)
```
