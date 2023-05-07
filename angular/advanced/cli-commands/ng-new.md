---
description: Creates a new workspace and an initial Angular app.
---

# ng new

```
ng new <name> [options]
ng n <name> [options]
```

### Arguments <a href="#arguments" id="arguments"></a>

| `<name>` | The name of the new workspace and initial project. |
| -------- | -------------------------------------------------- |

### Options <a href="#options" id="options"></a>

| OPTION                                                                                   | DESCRIPTION                                                                                                                                                                                                                                                                                                   |
| ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--collection=collection`                                                                | <p>A collection of schematics to use in generating the initial app.</p><p>Aliases: -c</p>                                                                                                                                                                                                                     |
| `--createApplication=true\|false`                                                        | <p>When true (the default), creates a new initial app project in the src folder of the new workspace. When false, creates an empty workspace with no initial app. You can then use the generate application command so that all apps are created in the projects folder.</p><p>Default: <code>true</code></p> |
| `--directory=directory`                                                                  | The directory name to create the workspace in.                                                                                                                                                                                                                                                                |
| `--dryRun=true\|false`                                                                   | <p>When true, runs through and reports activity without writing out results.</p><p>Default: <code>false</code></p><p>Aliases: -d</p>                                                                                                                                                                          |
| `--force=true\|false`                                                                    | <p>When true, forces overwriting of existing files.</p><p>Default: <code>false</code></p><p>Aliases: -f</p>                                                                                                                                                                                                   |
| `--newProjectRoot=newProjectRoot`                                                        | <p>The path where new projects will be created, relative to the new workspace root.</p><p>Default: <code>projects</code></p>                                                                                                                                                                                  |
| <p><code>--packageManager=</code><br> <code>npm|yarn|pnpm|cnpm</code></p>                | The package manager used to install dependencies.                                                                                                                                                                                                                                                             |
| `--prefix=prefix`                                                                        | <p>The prefix to apply to generated selectors for the initial project.</p><p>Default: <code>app</code></p><p>Aliases: -p</p>                                                                                                                                                                                  |
| `--routing=true\|false`                                                                  | When true, generates a routing module for the initial project.                                                                                                                                                                                                                                                |
| <p><code>--style=</code><br> <code>css|scss|sass|less|styl</code></p>                    | The file extension or preprocessor to use for style files.                                                                                                                                                                                                                                                    |
| `--verbose=true\|false`                                                                  | <p>When true, adds more details to output logging.</p><p>Default: <code>false</code></p><p>Aliases: -v</p>                                                                                                                                                                                                    |
| <p><code>--viewEncapsulation=</code><br> <code>Emulated|Native|None|ShadowDom</code></p> | The view encapsulation strategy to use in the initial project.                                                                                                                                                                                                                                                |
