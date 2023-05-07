---
description: >-
  The Angular CLI is a command-line interface tool that you use to initialize,
  develop, scaffold, and maintain Angular applications.
---

# CLI Commands

### Basic workflow <a href="#basic-workflow" id="basic-workflow"></a>

&#x20;Invoke the tool on the command line through the `ng` executable. Online help is available on the command line. Enter the following to list commands or options for a given command

```
ng help
ng generate --help
```

### Workspaces and project files <a href="#workspaces-and-project-files" id="workspaces-and-project-files"></a>

&#x20;The [ng new](https://angular.io/cli/new) command creates an _Angular workspace_ folder and generates a new app skeleton. A workspace can contain multiple apps and libraries. The initial app created by the [ng new](https://angular.io/cli/new) command is at the top level of the workspace. When you generate an additional app or library in a workspace, it goes into a `projects/` subfolder.

&#x20;A single workspace configuration file, `angular.json`, is created at the top level of the workspace.  The [ng config](https://angular.io/cli/config) command lets you set and retrieve configuration values from the command line, or you can edit the `angular.json` file directly.

### CLI command-language syntax <a href="#cli-command-language-syntax" id="cli-command-language-syntax"></a>

&#x20;`ng` _commandNameOrAlias_ _requiredArg_ \[_optionalArg_] `[options]`

* Most commands, and some options, have aliases. Aliases are shown in the syntax statement for each command.
* Option names are prefixed with a double dash (--). Option aliases are prefixed with a single dash (-). Arguments are not prefixed.
* Typically, the name of a generated artifact can be given as an argument to the command or specified with the --name option.
* Argument and option names can be given in either [camelCase or dash-case](https://angular.io/guide/glossary#case-types). `--myOptionName` is equivalent to `--my-option-name`.

