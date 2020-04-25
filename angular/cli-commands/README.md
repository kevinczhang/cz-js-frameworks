---
description: >-
  The Angular CLI is a command-line interface tool that you use to initialize,
  develop, scaffold, and maintain Angular applications.
---

# CLI Commands

### Basic workflow <a id="basic-workflow"></a>

 Invoke the tool on the command line through the `ng` executable. Online help is available on the command line. Enter the following to list commands or options for a given command

```
ng help
ng generate --help
```

### Workspaces and project files <a id="workspaces-and-project-files"></a>

 The [ng new](https://angular.io/cli/new) command creates an _Angular workspace_ folder and generates a new app skeleton. A workspace can contain multiple apps and libraries. The initial app created by the [ng new](https://angular.io/cli/new) command is at the top level of the workspace. When you generate an additional app or library in a workspace, it goes into a `projects/` subfolder.

 A single workspace configuration file, `angular.json`, is created at the top level of the workspace.  The [ng config](https://angular.io/cli/config) command lets you set and retrieve configuration values from the command line, or you can edit the `angular.json` file directly.



