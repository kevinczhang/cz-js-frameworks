---
description: Generates and/or modifies files based on a schematic.
---

# ng generate

## Common syntax

```text
ng generate <schematic> [options]
ng g <schematic> [options]
```



## ng g application

Generates a new basic app definition in the "projects" subfolder of the workspace.

#### **Arguments**

| ARGUMENT | DESCRIPTION |
| :--- | :--- |
| `<name>` | The name of the new app. |

#### **Options**

<table>
  <thead>
    <tr>
      <th style="text-align:left">OPTION</th>
      <th style="text-align:left">DESCRIPTION</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>--prefix=prefix</code>
      </td>
      <td style="text-align:left">
        <p>A prefix to apply to generated selectors.</p>
        <p>Default: <code>app</code>
        </p>
        <p>Aliases: -p</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--routing=true|false</code>
      </td>
      <td style="text-align:left">
        <p>When true, creates a routing NgModule.</p>
        <p>Default: <code>false</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--style=<br /> css|scss|sass|less|styl</code>
      </td>
      <td style="text-align:left">
        <p>The file extension or preprocessor to use for style files.</p>
        <p>Default: <code>css</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--viewEncapsulation=<br /> Emulated|Native|None|ShadowDom</code>
      </td>
      <td style="text-align:left">The view encapsulation strategy to use in the new app.</td>
    </tr>
  </tbody>
</table>## ng g class

Creates a new generic class definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION |
| :--- | :--- |
| `<name>` | The name of the new class. |

**Options**

<table>
  <thead>
    <tr>
      <th style="text-align:left">OPTION</th>
      <th style="text-align:left">DESCRIPTION</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>--project=project</code>
      </td>
      <td style="text-align:left">The name of the project.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--type=type</code>
      </td>
      <td style="text-align:left">
        <p>Adds a developer-defined type to the filename, in the format &quot;name.type.ts&quot;.</p>
        <p>Default:</p>
      </td>
    </tr>
  </tbody>
</table>## ng g component

Creates a new generic component definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION |
| :--- | :--- |
| `<name>` | The name of the component. |

**Options**

<table>
  <thead>
    <tr>
      <th style="text-align:left">OPTION</th>
      <th style="text-align:left">DESCRIPTION</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>--flat=true|false</code>
      </td>
      <td style="text-align:left">
        <p>When true, creates the new files at the top level of the current project.</p>
        <p>Default: <code>false</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--module=module</code>
      </td>
      <td style="text-align:left">
        <p>The declaring NgModule.</p>
        <p>Aliases: -m</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--prefix=prefix</code>
      </td>
      <td style="text-align:left">
        <p>The prefix to apply to the generated component selector.</p>
        <p>Aliases: -p</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--project=project</code>
      </td>
      <td style="text-align:left">The name of the project.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--selector=selector</code>
      </td>
      <td style="text-align:left">The HTML selector to use for this component.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--style=<br /> css|scss|sass|less|styl</code>
      </td>
      <td style="text-align:left">
        <p>The file extension or preprocessor to use for style files.</p>
        <p>Default: <code>css</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--type=type</code>
      </td>
      <td style="text-align:left">
        <p>Adds a developer-defined type to the filename, in the format &quot;name.type.ts&quot;.</p>
        <p>Default: <code>Component</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--viewEncapsulation=<br /> Emulated|Native|None|ShadowDom</code>
      </td>
      <td style="text-align:left">
        <p>The view encapsulation strategy to use in the new component.</p>
        <p>Aliases: -v</p>
      </td>
    </tr>
  </tbody>
</table>## ng g directive

Creates a new generic directive definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION |
| :--- | :--- |
| `<name>` | The name of the new directive. |

**Options**

<table>
  <thead>
    <tr>
      <th style="text-align:left">OPTION</th>
      <th style="text-align:left">DESCRIPTION</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>--flat=true|false</code>
      </td>
      <td style="text-align:left">
        <p>When true (the default), creates the new files at the top level of the
          current project.</p>
        <p>Default: <code>true</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--module=module</code>
      </td>
      <td style="text-align:left">
        <p>The declaring NgModule.</p>
        <p>Aliases: -m</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--prefix=prefix</code>
      </td>
      <td style="text-align:left">
        <p>A prefix to apply to generated selectors.</p>
        <p>Aliases: -p</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--project=project</code>
      </td>
      <td style="text-align:left">The name of the project.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--selector=selector</code>
      </td>
      <td style="text-align:left">The HTML selector to use for this directive.</td>
    </tr>
  </tbody>
</table>## ng g enum

Generates a new, generic enum definition for the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION |
| :--- | :--- |
| `<name>` | The name of the enum. |

**Options**

| OPTION | DESCRIPTION |
| :--- | :--- |
| `--project=project` | The name of the project in which to create the enum. Default is the configured default project for the workspace. |

## ng g guard

Generates a new, generic route guard definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION |
| :--- | :--- |
| `<name>` | The name of the new route guard. |

**Options**

<table>
  <thead>
    <tr>
      <th style="text-align:left">OPTION</th>
      <th style="text-align:left">DESCRIPTION</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>--flat=true|false</code>
      </td>
      <td style="text-align:left">
        <p>When true (the default), creates the new files at the top level of the
          current project.</p>
        <p>Default: <code>true</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--implements</code>
      </td>
      <td style="text-align:left">Specifies which interfaces to implement.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--project=project</code>
      </td>
      <td style="text-align:left">The name of the project.</td>
    </tr>
  </tbody>
</table>## ng g interceptor

Creates a new, generic interceptor definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION |
| :--- | :--- |
| `<name>` | The name of the interceptor. |

**Options**

<table>
  <thead>
    <tr>
      <th style="text-align:left">OPTION</th>
      <th style="text-align:left">DESCRIPTION</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>--flat=true|false</code>
      </td>
      <td style="text-align:left">
        <p>When true (the default), creates files at the top level of the project.</p>
        <p>Default: <code>true</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--project=project</code>
      </td>
      <td style="text-align:left">The name of the project.</td>
    </tr>
  </tbody>
</table>## ng g interface

Creates a new generic interface definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION |
| :--- | :--- |
| `<name>` | The name of the interface. |
| `<type>` | Adds a developer-defined type to the filename, in the format "name.type.ts". |

**Options**

<table>
  <thead>
    <tr>
      <th style="text-align:left">OPTION</th>
      <th style="text-align:left">DESCRIPTION</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>--prefix=prefix</code>
      </td>
      <td style="text-align:left">
        <p>A prefix to apply to generated selectors.</p>
        <p>Default:</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--project=project</code>
      </td>
      <td style="text-align:left">The name of the project.</td>
    </tr>
  </tbody>
</table>## ng g library

Creates a new generic library project in the current workspace.

**Arguments**

| ARGUMENT | DESCRIPTION |
| :--- | :--- |
| `<name>` | The name of the library. |

**Options**

<table>
  <thead>
    <tr>
      <th style="text-align:left">OPTION</th>
      <th style="text-align:left">DESCRIPTION</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>--entryFile=entryFile</code>
      </td>
      <td style="text-align:left">
        <p>The path at which to create the library&apos;s public API file, relative
          to the workspace root.</p>
        <p>Default: <code>public-api</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--prefix=prefix</code>
      </td>
      <td style="text-align:left">
        <p>A prefix to apply to generated selectors.</p>
        <p>Default: <code>lib</code>
        </p>
        <p>Aliases: -p</p>
      </td>
    </tr>
  </tbody>
</table>## ng g module

Creates a new generic NgModule definition in the given or default project.

**Arguments**

| ARGUMENT | DESCRIPTION |
| :--- | :--- |
| `<name>` | The name of the NgModule. |

**Options**

<table>
  <thead>
    <tr>
      <th style="text-align:left">OPTION</th>
      <th style="text-align:left">DESCRIPTION</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>--flat=true|false</code>
      </td>
      <td style="text-align:left">
        <p>When true, creates the new files at the top level of the current project
          root.</p>
        <p>Default: <code>false</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--module=module</code>
      </td>
      <td style="text-align:left">
        <p>The declaring NgModule.</p>
        <p>Aliases: -m</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--project=project</code>
      </td>
      <td style="text-align:left">The name of the project.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--route=route</code>
      </td>
      <td style="text-align:left">The route path for a lazy-loaded module. When supplied, creates a component
        in the new module, and adds the route to that component in the <a href="https://angular.io/api/router/Routes"><code>Routes</code></a> array
        declared in the module provided in the <code>--module</code> option.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--routing=true|false</code>
      </td>
      <td style="text-align:left">
        <p>When true, creates a routing module.</p>
        <p>Default: <code>false</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--routingScope=Child|Root</code>
      </td>
      <td style="text-align:left">
        <p>The scope for the new routing module.</p>
        <p>Default: <code>Child</code>
        </p>
      </td>
    </tr>
  </tbody>
</table>