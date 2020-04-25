---
description: >-
  Generates a new basic app definition in the "projects" subfolder of the
  workspace.
---

# application

```text
ng generate application <name> [options]
ng g application <name> [options]
```

## **Arguments**

| ARGUMENT | DESCRIPTION |
| :--- | :--- |
| `<name>` | The name of the new app. |

## **Options**

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
</table>

