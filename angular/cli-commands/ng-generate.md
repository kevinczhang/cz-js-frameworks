---
description: Generates and/or modifies files based on a schematic.
---

# ng generate

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
</table>