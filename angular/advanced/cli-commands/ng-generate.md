---
description: Generates and/or modifies files based on a schematic.
---

# ng generate

## Common syntax

```
ng generate <schematic> [options]
ng g <schematic> [options]
```



## ng g application

Generates a new basic app definition in the "projects" subfolder of the workspace.

#### **Arguments**

| ARGUMENT | DESCRIPTION              |
| -------- | ------------------------ |
| `<name>` | The name of the new app. |

#### **Options**

| OPTION                                                                                   | DESCRIPTION                                                                                        |
| ---------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `--prefix=prefix`                                                                        | <p>A prefix to apply to generated selectors.</p><p>Default: <code>app</code></p><p>Aliases: -p</p> |
| `--routing=true\|false`                                                                  | <p>When true, creates a routing NgModule.</p><p>Default: <code>false</code></p>                    |
| <p><code>--style=</code><br> <code>css|scss|sass|less|styl</code></p>                    | <p>The file extension or preprocessor to use for style files.</p><p>Default: <code>css</code></p>  |
| <p><code>--viewEncapsulation=</code><br> <code>Emulated|Native|None|ShadowDom</code></p> | The view encapsulation strategy to use in the new app.                                             |

## ng g class

Creates a new generic class definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION                |
| -------- | -------------------------- |
| `<name>` | The name of the new class. |

**Options**

| OPTION              | DESCRIPTION                                                                                        |
| ------------------- | -------------------------------------------------------------------------------------------------- |
| `--project=project` | The name of the project.                                                                           |
| `--type=type`       | <p>Adds a developer-defined type to the filename, in the format "name.type.ts".</p><p>Default:</p> |

## ng g component

Creates a new generic component definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION                |
| -------- | -------------------------- |
| `<name>` | The name of the component. |

**Options**

| OPTION                                                                                   | DESCRIPTION                                                                                                               |
| ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `--flat=true\|false`                                                                     | <p>When true, creates the new files at the top level of the current project.</p><p>Default: <code>false</code></p>        |
| `--module=module`                                                                        | <p>The declaring NgModule.</p><p>Aliases: -m</p>                                                                          |
| `--prefix=prefix`                                                                        | <p>The prefix to apply to the generated component selector.</p><p>Aliases: -p</p>                                         |
| `--project=project`                                                                      | The name of the project.                                                                                                  |
| `--selector=selector`                                                                    | The HTML selector to use for this component.                                                                              |
| <p><code>--style=</code><br> <code>css|scss|sass|less|styl</code></p>                    | <p>The file extension or preprocessor to use for style files.</p><p>Default: <code>css</code></p>                         |
| `--type=type`                                                                            | <p>Adds a developer-defined type to the filename, in the format "name.type.ts".</p><p>Default: <code>Component</code></p> |
| <p><code>--viewEncapsulation=</code><br> <code>Emulated|Native|None|ShadowDom</code></p> | <p>The view encapsulation strategy to use in the new component.</p><p>Aliases: -v</p>                                     |

## ng g directive

Creates a new generic directive definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION                    |
| -------- | ------------------------------ |
| `<name>` | The name of the new directive. |

**Options**

| OPTION                | DESCRIPTION                                                                                                                     |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `--flat=true\|false`  | <p>When true (the default), creates the new files at the top level of the current project.</p><p>Default: <code>true</code></p> |
| `--module=module`     | <p>The declaring NgModule.</p><p>Aliases: -m</p>                                                                                |
| `--prefix=prefix`     | <p>A prefix to apply to generated selectors.</p><p>Aliases: -p</p>                                                              |
| `--project=project`   | The name of the project.                                                                                                        |
| `--selector=selector` | The HTML selector to use for this directive.                                                                                    |

## ng g enum

Generates a new, generic enum definition for the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION           |
| -------- | --------------------- |
| `<name>` | The name of the enum. |

**Options**

| OPTION              | DESCRIPTION                                                                                                       |
| ------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `--project=project` | The name of the project in which to create the enum. Default is the configured default project for the workspace. |

## ng g guard

Generates a new, generic route guard definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION                      |
| -------- | -------------------------------- |
| `<name>` | The name of the new route guard. |

**Options**

| OPTION               | DESCRIPTION                                                                                                                     |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `--flat=true\|false` | <p>When true (the default), creates the new files at the top level of the current project.</p><p>Default: <code>true</code></p> |
| `--implements`       | Specifies which interfaces to implement.                                                                                        |
| `--project=project`  | The name of the project.                                                                                                        |

## ng g interceptor

Creates a new, generic interceptor definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION                  |
| -------- | ---------------------------- |
| `<name>` | The name of the interceptor. |

**Options**

| OPTION               | DESCRIPTION                                                                                                     |
| -------------------- | --------------------------------------------------------------------------------------------------------------- |
| `--flat=true\|false` | <p>When true (the default), creates files at the top level of the project.</p><p>Default: <code>true</code></p> |
| `--project=project`  | The name of the project.                                                                                        |

## ng g interface

Creates a new generic interface definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION                                                                  |
| -------- | ---------------------------------------------------------------------------- |
| `<name>` | The name of the interface.                                                   |
| `<type>` | Adds a developer-defined type to the filename, in the format "name.type.ts". |

**Options**

| OPTION              | DESCRIPTION                                                     |
| ------------------- | --------------------------------------------------------------- |
| `--prefix=prefix`   | <p>A prefix to apply to generated selectors.</p><p>Default:</p> |
| `--project=project` | The name of the project.                                        |

## ng g library

Creates a new generic library project in the current workspace.

**Arguments**

| ARGUMENT | DESCRIPTION              |
| -------- | ------------------------ |
| `<name>` | The name of the library. |

**Options**

| OPTION                  | DESCRIPTION                                                                                                                              |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `--entryFile=entryFile` | <p>The path at which to create the library's public API file, relative to the workspace root.</p><p>Default: <code>public-api</code></p> |
| `--prefix=prefix`       | <p>A prefix to apply to generated selectors.</p><p>Default: <code>lib</code></p><p>Aliases: -p</p>                                       |

## ng g module

Creates a new generic NgModule definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION               |
| -------- | ------------------------- |
| `<name>` | The name of the NgModule. |

**Options**

| OPTION                       | DESCRIPTION                                                                                                                                                                                                                                                 |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--flat=true\|false`         | <p>When true, creates the new files at the top level of the current project root.</p><p>Default: <code>false</code></p>                                                                                                                                     |
| `--module=module`            | <p>The declaring NgModule.</p><p>Aliases: -m</p>                                                                                                                                                                                                            |
| `--project=project`          | The name of the project.                                                                                                                                                                                                                                    |
| `--route=route`              | The route path for a lazy-loaded module. When supplied, creates a component in the new module, and adds the route to that component in the [`Routes`](https://angular.io/api/router/Routes) array declared in the module provided in the `--module` option. |
| `--routing=true\|false`      | <p>When true, creates a routing module.</p><p>Default: <code>false</code></p>                                                                                                                                                                               |
| `--routingScope=Child\|Root` | <p>The scope for the new routing module.</p><p>Default: <code>Child</code></p>                                                                                                                                                                              |

## ng g pipe

Creates a new generic pipe definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION           |
| -------- | --------------------- |
| `<name>` | The name of the pipe. |

**Options**

| OPTION                 | DESCRIPTION                                                                                                    |
| ---------------------- | -------------------------------------------------------------------------------------------------------------- |
| `--export=true\|false` | <p>When true, the declaring NgModule exports this pipe.</p><p>Default: <code>false</code></p>                  |
| `--flat=true\|false`   | <p>When true (the default) creates files at the top level of the project.</p><p>Default: <code>true</code></p> |
| `--module=module`      | <p>The declaring NgModule.</p><p>Aliases: -m</p>                                                               |
| `--project=project`    | The name of the project.                                                                                       |

## ng g service

Creates a new, generic service definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION              |
| -------- | ------------------------ |
| `<name>` | The name of the service. |

**Options**

| OPTION               | DESCRIPTION                                                                                                     |
| -------------------- | --------------------------------------------------------------------------------------------------------------- |
| `--flat=true\|false` | <p>When true (the default), creates files at the top level of the project.</p><p>Default: <code>true</code></p> |
| `--project=project`  | The name of the project.                                                                                        |

