![](https://cloud.githubusercontent.com/assets/110953/7877439/6a69d03e-0590-11e5-9fac-c614246606de.png)
## My portfolio

> My starting point for building web applications with Polymer 1.0 starter kit.

### For learning Polymer some tutorials

Check out the Polymer Starter Kit tutorials on [polymer-project.org](https://www.polymer-project.org):

* [Set up the PSK](https://www.polymer-project.org/1.0/docs/start/psk/set-up.html)
* [Create a page](https://www.polymer-project.org/1.0/docs/start/psk/create-a-page.html)
* [Deploy the PSK to the web](https://www.polymer-project.org/1.0/docs/start/psk/deploy.html)

## Getting Started

To take advantage of this Kit you need to:

1. Get a copy of the code.
2. Install the dependencies if you don't already have them.
3. Modify the application to your liking.
4. Deploy your production code.

### Get the code

Clone the repo 

```sh
git clone https://github.com/sounakpal/portfolio.git
```

### Install dependencies

#### Quick-start (for experienced users)

With Node.js installed, run the following one liner from the root of your Polymer Starter Kit download:

```sh
npm install -g gulp bower && npm install && bower install
```

#### Prerequisites (for everyone)

The full starter kit requires the following major dependencies:

- Node.js, used to run JavaScript tools from the command line.
- npm, the node package manager, installed with Node.js and used to install Node.js packages.
- gulp, a Node.js-based build tool.
- bower, a Node.js-based package manager used to install front-end packages (like Polymer).

**To install dependencies:**

1)  Check your Node.js version.

```sh
node --version
```

The version should be at or above 0.12.x.

2)  If you don't have Node.js installed, or you have a lower version, go to [nodejs.org](https://nodejs.org) and click on the big green Install button.

3)  Install `gulp` and `bower` globally.

```sh
npm install -g gulp bower
```

This lets you run `gulp` and `bower` from the command line.

4)  Install the starter kit's local `npm` and `bower` dependencies.

```sh
cd polymer-starter-kit && npm install && bower install
```

This installs the element sets (Paper, Iron, Platinum) and tools the starter kit requires to build and serve apps.

### Development workflow

#### Serve / watch

```sh
gulp serve
```

This outputs an IP address you can use to locally test and another that can be used on devices connected to your network.

#### Run tests

```sh
gulp test:local
```

This runs the unit tests defined in the `app/test` directory through [web-component-tester](https://github.com/Polymer/web-component-tester).

To run tests Java 7 or higher is required. To update Java go to http://www.oracle.com/technetwork/java/javase/downloads/index.html and download ***JDK*** and install it.

#### Build & Vulcanize

```sh
gulp
```

Build and optimize the current project, ready for deployment. This includes linting as well as vulcanization, image, script, stylesheet and HTML optimization and minification.

## Application Theming & Styling

Polymer 1.0 introduces a shim for CSS custom properties. We take advantage of this in `app/styles/app-theme.html` to provide theming for your application. You can also find our presets for Material Design breakpoints in this file.

[Read more](https://www.polymer-project.org/1.0/docs/devguide/styling.html) about CSS custom properties.

### Styling
1. ***main.css*** - to define styles that can be applied outside of Polymer's custom CSS properties implementation. Some of the use-cases include defining styles that you want to be applied for a splash screen, styles for your application 'shell' before it gets upgraded using Polymer or critical style blocks that you want parsed before your elements are.
2. ***app-theme.html*** - to provide theming for your application. You can also find our presets for Material Design breakpoints in this file.
3. ***shared-styles.html*** - to share styles between elements and index.html.
4. ***element styles only*** - styles specific to element. These styles should be inside the `<style></style>` inside `template`.

  ```HTML
  <dom-module id="my-list">
    <template>
      <style>
        :host {
          display: block;
          background-color: yellow;
        }
      </style>
      <ul>
        <template is="dom-repeat" items="{{items}}">
          <li><span class="paper-font-body1">{{item}}</span></li>
        </template>
      </ul>
    </template>
  </dom-module>
  ```

These style files are located in the [styles folder](app/styles/).

## Unit Testing

Web apps built with Polymer Starter Kit come configured with support for [Web Component Tester](https://github.com/Polymer/web-component-tester) - Polymer's preferred tool for authoring and running unit tests. This makes testing your element based applications a pleasant experience.

[Read more](https://github.com/Polymer/web-component-tester#html-suites) about using Web Component tester.

## Dependency Management

Polymer uses [Bower](http://bower.io) for package management. This makes it easy to keep your elements up to date and versioned. For tooling, we use npm to manage Node.js-based dependencies.

Components installed by Bower live in the `app/bower_components` directory. This location is specified by the `.bowerrc` file. Many projects which follow Yeoman conventions place the `bower_components` directory outside of the `app` directory and then mount it using a server. This causes problems for tools like [Vulcanize](https://github.com/polymer/vulcanize) and [web-component-shards](https://github.com/PolymerLabs/web-component-shards) which rely on relative paths. We've chosen to simplify things and have `bower_components` live inside of `app` to resolve these issues.

## Deploy

### Github Pages

1. Uncomment this line  `// app.baseUrl = '/polymer-starter-kit/';` in app.js near the top
2. Change `app.baseUrl = '/polymer-starter-kit/';`  to `app.baseUrl = '/your-pathname/';` (ex: if you repo is `github.com/username/bobs-awesome-site` you would change this to `bobs-awesome-site`)
3. Run `gulp build-deploy-gh-pages` from command line
4. To see changes wait 1-2 minutes then load Github pages for your app (ex: https://polymerelements.github.io/polymer-starter-kit/)

[See more details](/docs/deploy-to-github-pages.md/)

### Firebase

[See detail recipe](/docs/deploy-to-firebase-pretty-urls.md/)

## Service Worker

Polymer Starter Kit offers an optional offline experience thanks to Service Worker and the [Platinum Service Worker elements](https://github.com/PolymerElements/platinum-sw). New to Service Worker? Read the following [introduction](http://www.html5rocks.com/en/tutorials/service-worker/introduction/) to understand how it works.

Our optional offline setup should work well for relatively simple applications. For more complex apps, we recommend learning how Service Worker works so that you can make the most of the Platinum Service Worker element abstractions.

### Enable Service Worker support?

To enable Service Worker support for Polymer Starter Kit project use these 3 steps:

1. Uncomment Service Worker code in index.html
  ```HTML
  <!-- Uncomment next block to enable Service Worker support (1/2) -->
  <!--
  <paper-toast id="caching-complete"
               duration="6000"
               text="Caching complete! This app will work offline.">
  </paper-toast>

  <platinum-sw-register auto-register
                        clients-claim
                        skip-waiting
                        on-service-worker-installed="displayInstalledToast">
    <platinum-sw-cache default-cache-strategy="networkFirst"
                       cache-config-file="cache-config.json">
    </platinum-sw-cache>
  </platinum-sw-register>
  -->
  ```
2. Uncomment Service Worker code in elements.html

  ```HTML
  <!-- Uncomment next block to enable Service Worker Support (2/2) -->
  <!--
  <link rel="import" href="../bower_components/platinum-sw/platinum-sw-cache.html">
  <link rel="import" href="../bower_components/platinum-sw/platinum-sw-register.html">
  -->
  ```
3. Uncomment 'cache-config' in the `runSequence()` section of the 'default' gulp task, like below:
[(gulpfile.js)](https://github.com/PolymerElements/polymer-starter-kit/blob/master/gulpfile.js)

  ```JavaScript
  // Build Production Files, the Default Task
  gulp.task('default', ['clean'], function (cb) {
    runSequence(
      ['copy', 'styles'],
      'elements',
      ['jshint', 'images', 'fonts', 'html'],
      'vulcanize', 'cache-config',
      cb);
  });
  ```


## Contributing

Polymer Starter Kit is a new project and is an ongoing effort by the Web Component community. We welcome your bug reports, PRs for improvements, docs and anything you think would improve the experience for other Polymer developers.
