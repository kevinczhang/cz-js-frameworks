---
description: Creates a new workspace and an initial Angular app.
---

# ng new

```text
ng new <name> [options]
ng n <name> [options]
```

### Arguments <a id="arguments"></a>

| `<name>` | The name of the new workspace and initial project. |
| :--- | :--- |


### Options <a id="options"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left">OPTION</th>
      <th style="text-align:left">DESCRIPTION</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>--collection=collection</code>
      </td>
      <td style="text-align:left">
        <p>A collection of schematics to use in generating the initial app.</p>
        <p>Aliases: -c</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--createApplication=true|false</code>
      </td>
      <td style="text-align:left">
        <p>When true (the default), creates a new initial app project in the src
          folder of the new workspace. When false, creates an empty workspace with
          no initial app. You can then use the generate application command so that
          all apps are created in the projects folder.</p>
        <p>Default: <code>true</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--directory=directory</code>
      </td>
      <td style="text-align:left">The directory name to create the workspace in.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--dryRun=true|false</code>
      </td>
      <td style="text-align:left">
        <p>When true, runs through and reports activity without writing out results.</p>
        <p>Default: <code>false</code>
        </p>
        <p>Aliases: -d</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--force=true|false</code>
      </td>
      <td style="text-align:left">
        <p>When true, forces overwriting of existing files.</p>
        <p>Default: <code>false</code>
        </p>
        <p>Aliases: -f</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--newProjectRoot=newProjectRoot</code>
      </td>
      <td style="text-align:left">
        <p>The path where new projects will be created, relative to the new workspace
          root.</p>
        <p>Default: <code>projects</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--packageManager=<br /> npm|yarn|pnpm|cnpm</code>
      </td>
      <td style="text-align:left">The package manager used to install dependencies.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--prefix=prefix</code>
      </td>
      <td style="text-align:left">
        <p>The prefix to apply to generated selectors for the initial project.</p>
        <p>Default: <code>app</code>
        </p>
        <p>Aliases: -p</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--routing=true|false</code>
      </td>
      <td style="text-align:left">When true, generates a routing module for the initial project.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--style=<br /> css|scss|sass|less|styl</code>
      </td>
      <td style="text-align:left">The file extension or preprocessor to use for style files.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--verbose=true|false</code>
      </td>
      <td style="text-align:left">
        <p>When true, adds more details to output logging.</p>
        <p>Default: <code>false</code>
        </p>
        <p>Aliases: -v</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>--viewEncapsulation=<br /> Emulated|Native|None|ShadowDom</code>
      </td>
      <td style="text-align:left">The view encapsulation strategy to use in the initial project.</td>
    </tr>
  </tbody>
</table>