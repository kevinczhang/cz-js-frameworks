---
description: The following table summarizes the @NgModule metadata properties.
---

# NgModule metadata

<table>
  <thead>
    <tr>
      <th style="text-align:left">Property</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><a href="https://angular.io/api/core/NgModule#declarations"><code>declarations</code></a>
      </td>
      <td style="text-align:left">
        <p>A list of <a href="https://angular.io/guide/ngmodule-faq#q-declarable">declarable</a> classes,
          (<em>components</em>, <em>directives</em>, and <em>pipes</em>) that <em>belong to this module</em>.</p>
        <ol>
          <li>When compiling a template, you need to determine a set of selectors which
            should be used for triggering their corresponding directives.</li>
          <li>The template is compiled within the context of an NgModule&#x2014;the
            NgModule within which the template&apos;s component is declared&#x2014;which
            determines the set of selectors using the following rules:
            <ul>
              <li>All selectors of directives listed in `declarations`.</li>
              <li>All selectors of directives exported from imported NgModules.</li>
            </ul>
          </li>
        </ol>
        <p>Components, directives, and pipes must belong to <em>exactly</em> one module.
          The compiler emits an error if you try to declare the same class in more
          than one module. Be careful not to re-declare a class that is imported
          directly or indirectly from another module.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>providers</code>
      </td>
      <td style="text-align:left">
        <p>A list of dependency-injection providers.</p>
        <p>Angular registers these providers with the NgModule&apos;s injector. If
          it is the NgModule used for bootstrapping then it is the root injector.</p>
        <p>These services become available for injection into any component, directive,
          pipe or service which is a child of this injector.</p>
        <p>A lazy-loaded module has its own injector which is typically a child of
          the application root injector.</p>
        <p>Lazy-loaded services are scoped to the lazy module&apos;s injector. If
          a lazy-loaded module also provides the <code>UserService</code>, any component
          created within that module&apos;s context (such as by router navigation)
          gets the local instance of the service, not the instance in the root application
          injector.</p>
        <p>Components in external modules continue to receive the instance provided
          by their injectors.</p>
        <p>For more information on injector hierarchy and scoping, see <a href="https://angular.io/guide/providers">Providers</a> and
          the <a href="https://angular.io/guide/dependency-injection">DI Guide</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://angular.io/api/core/NgModule#imports"><code>imports</code></a>
      </td>
      <td style="text-align:left">
        <p>A list of modules which should be folded into this module. Folded means
          it is as if all the imported NgModule&apos;s exported properties were declared
          here.</p>
        <p>Specifically, it is as if the list of modules whose exported components,
          directives, or pipes are referenced by the component templates were declared
          in this module.</p>
        <p>A component template can <a href="https://angular.io/guide/ngmodule-faq#q-template-reference">reference</a> another
          component, directive, or pipe when the reference is declared in this module
          or if the imported module has exported it. For example, a component can
          use the <a href="https://angular.io/api/common/NgIf"><code>NgIf</code></a> and <code>NgFor</code>directives
          only if the module has imported the Angular <a href="https://angular.io/api/common/CommonModule"><code>CommonModule</code></a>(perhaps
          indirectly by importing <a href="https://angular.io/api/platform-browser/BrowserModule"><code>BrowserModule</code></a>).</p>
        <p>You can import many standard directives from the <a href="https://angular.io/api/common/CommonModule"><code>CommonModule</code></a> but
          some familiar directives belong to other modules. For example, you can
          use <code>[(</code><a href="https://angular.io/api/forms/NgModel"><code>ngModel</code></a><code>)]</code> only
          after importing the Angular <a href="https://angular.io/api/forms/FormsModule"><code>FormsModule</code></a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://angular.io/api/core/NgModule#exports"><code>exports</code></a>
      </td>
      <td style="text-align:left">
        <p>A list of declarations&#x2014;<em>component</em>, <em>directive</em>, and <em>pipe</em> classes&#x2014;that
          an importing module can use.</p>
        <p>Exported declarations are the module&apos;s <em>public API</em>. A component
          in another module can <a href="https://angular.io/guide/ngmodule-faq#q-template-reference">use</a>  <em>this</em> module&apos;s <code>UserComponent</code> if
          it imports this module and this module exports <code>UserComponent</code>.</p>
        <p>Declarations are private by default. If this module does <em>not</em> export <code>UserComponent</code>,
          then only the components within <em>this</em> module can use <code>UserComponent</code>.</p>
        <p>Importing a module does <em>not</em> automatically re-export the imported
          module&apos;s imports. Module &apos;B&apos; can&apos;t use <a href="https://angular.io/api/common/NgIf"><code>ngIf</code></a> just
          because it imported module &apos;A&apos; which imported <a href="https://angular.io/api/common/CommonModule"><code>CommonModule</code></a>.
          Module &apos;B&apos; must import <a href="https://angular.io/api/common/CommonModule"><code>CommonModule</code></a> itself.</p>
        <p>A module can list another module among its <a href="https://angular.io/api/core/NgModule#exports"><code>exports</code></a>,
          in which case all of that module&apos;s public components, directives,
          and pipes are exported.</p>
        <p><a href="https://angular.io/guide/ngmodule-faq#q-reexport">Re-export</a> makes
          module transitivity explicit. If Module &apos;A&apos; re-exports <a href="https://angular.io/api/common/CommonModule"><code>CommonModule</code></a> and
          Module &apos;B&apos; imports Module &apos;A&apos;, Module &apos;B&apos;
          components can use <a href="https://angular.io/api/common/NgIf"><code>ngIf</code></a> even
          though &apos;B&apos; itself didn&apos;t import <a href="https://angular.io/api/common/CommonModule"><code>CommonModule</code></a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://angular.io/api/core/NgModule#bootstrap"><code>bootstrap</code></a>
      </td>
      <td style="text-align:left">
        <p>A list of components that are automatically bootstrapped.</p>
        <p>Usually there&apos;s only one component in this list, the <em>root component</em> of
          the application.</p>
        <p>Angular can launch with multiple bootstrap components, each with its own
          location in the host web page.</p>
        <p>A bootstrap component is automatically added to <code>entryComponents</code>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>entryComponents</code>
      </td>
      <td style="text-align:left">
        <p>A list of components that can be dynamically loaded into the view.</p>
        <p>By default, an Angular app always has at least one entry component, the
          root component, <code>AppComponent</code>. Its purpose is to serve as a
          point of entry into the app, that is, you bootstrap it to launch the app.</p>
        <p>Routed components are also <em>entry components</em> because they need to
          be loaded dynamically. The router creates them and drops them into the
          DOM near a <code>&lt;</code><a href="https://angular.io/api/router/RouterOutlet"><code>router-outlet</code></a><code>&gt;</code>.</p>
        <p>While the bootstrapped and routed components are <em>entry components</em>,
          you don&apos;t have to add them to a module&apos;s <code>entryComponents</code> list,
          as they are added implicitly.</p>
        <p>Angular automatically adds components in the module&apos;s <a href="https://angular.io/api/core/NgModule#bootstrap"><code>bootstrap</code></a> and
          route definitions into the <code>entryComponents</code> list.</p>
        <p>That leaves only components bootstrapped using one of the imperative techniques,
          such as <a href="https://angular.io/api/core/ViewContainerRef#createComponent"><code>ViewComponentRef.createComponent()</code></a> as
          undiscoverable.</p>
        <p>Dynamic component loading is not common in most apps beyond the router.
          If you need to dynamically load components, you must add these components
          to the <code>entryComponents</code> list yourself.</p>
        <p>For more information, see <a href="https://angular.io/guide/entry-components">Entry Components</a>.</p>
      </td>
    </tr>
  </tbody>
</table>