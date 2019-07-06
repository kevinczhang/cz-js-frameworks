# Feature Modules

## Categories of feature modules

There are five general categories of feature modules which tend to fall into the following groups:

* Domain feature modules.
* Routed feature modules.
* Routing modules.
* Service feature modules.
* Widget feature modules.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Feature Module</th>
      <th style="text-align:left">Guidelines</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Domain</td>
      <td style="text-align:left">
        <p>Domain feature modules deliver a user experience dedicated to a particular
          application domain like editing a customer or placing an order.</p>
        <p>They typically have a top component that acts as the feature root and
          private, supporting sub-components descend from it.</p>
        <p>Domain feature modules consist mostly of declarations. Only the top component
          is exported.</p>
        <p>Domain feature modules rarely have providers. When they do, the lifetime
          of the provided services should be the same as the lifetime of the module.</p>
        <p>Domain feature modules are typically imported exactly once by a larger
          feature module.</p>
        <p>They might be imported by the root <code>AppModule</code> of a small application
          that lacks routing.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Routed</td>
      <td style="text-align:left">
        <p>Routed feature modules are domain feature modules whose top components
          are the targets of router navigation routes.</p>
        <p>All lazy-loaded modules are routed feature modules by definition.</p>
        <p>Routed feature modules don&#x2019;t export anything because their components
          never appear in the template of an external component.</p>
        <p>A lazy-loaded routed feature module should not be imported by any module.
          Doing so would trigger an eager load, defeating the purpose of lazy loading.That
          means you won&#x2019;t see them mentioned among the <code>AppModule</code> imports.
          An eager loaded routed feature module must be imported by another module
          so that the compiler learns about its components.</p>
        <p>Routed feature modules rarely have providers for reasons explained in
          <a
          href="https://angular.io/guide/lazy-loading-ngmodules">Lazy Loading Feature Modules</a>. When they do, the lifetime of the provided
            services should be the same as the lifetime of the module. Don&apos;t provide
            application-wide singleton services in a routed feature module or in a
            module that the routed module imports.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Routing</td>
      <td style="text-align:left">
        <p>A routing module provides routing configuration for another module and
          separates routing concerns from its companion module.</p>
        <p>A routing module typically does the following:</p>
        <ul>
          <li>Defines routes.</li>
          <li>Adds router configuration to the module&apos;s imports.</li>
          <li>Adds guard and resolver service providers to the module&apos;s providers.</li>
          <li>The name of the routing module should parallel the name of its companion
            module, using the suffix &quot;Routing&quot;. For example, <code>FooModule</code> in <code>foo.module.ts</code>has
            a routing module named <code>FooRoutingModule</code> in <code>foo-routing.module.ts</code>.
            If the companion module is the root <code>AppModule</code>, the <code>AppRoutingModule</code> adds
            router configuration to its imports with <code>RouterModule.forRoot(routes)</code>.
            All other routing modules are children that import <code>RouterModule.forChild(routes)</code>.</li>
          <li>A routing module re-exports the <a href="https://angular.io/api/router/RouterModule"><code>RouterModule</code></a> as
            a convenience so that components of the companion module have access to
            router directives such as <a href="https://angular.io/api/router/RouterLink"><code>RouterLink</code></a> and
            <a
            href="https://angular.io/api/router/RouterOutlet"><code>RouterOutlet</code>
              </a>.</li>
          <li>A routing module does not have its own declarations. Components, directives,
            and pipes are the responsibility of the feature module, not the routing
            module.</li>
        </ul>
        <p>A routing module should only be imported by its companion module.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Service</td>
      <td style="text-align:left">
        <p>Service modules provide utility services such as data access and messaging.
          Ideally, they consist entirely of providers and have no declarations. Angular&apos;s
          <a
          href="https://angular.io/api/common/http/HttpClientModule"><code>HttpClientModule</code>
            </a>is a good example of a service module.</p>
        <p>The root <code>AppModule</code> is the only module that should import service
          modules.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Widget</td>
      <td style="text-align:left">
        <p>A widget module makes components, directives, and pipes available to external
          modules. Many third-party UI component libraries are widget modules.</p>
        <p>A widget module should consist entirely of declarations, most of them
          exported.</p>
        <p>A widget module should rarely have providers.</p>
        <p>Import widget modules in any module whose component templates need the
          widgets.</p>
      </td>
    </tr>
  </tbody>
</table>| Feature Module | Declarations | Providers | Exports | Imported by |
| :--- | :--- | :--- | :--- | :--- |
| Domain | Yes | Rare | Top component | Feature, AppModule |
| Routed | Yes | Rare | No | None |
| Routing | No | Yes \(Guards\) | RouterModule | Feature \(for routing\) |
| Service | No | Yes | No | AppModule |
| Widget | Yes | Rare | Yes | Feature |

