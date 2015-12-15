# Bower Github Subdirectory Resolver

*Note: This is still a work in progress :)*

This is a [Bower Pluggable Resolver](http://bower.io/docs/pluggable-resolvers/)
that allows installation of bower modules from a subdirectory of a GitHub
repository.

For example, let's assume user `githubUser` has the following repo hosted on
GitHub:

```
repo/
  namespace/
    module/
      bower.json
      src/
    another-module/
      bower.json
      src/
```

A normal bower github installation (`bower install githubUser/repo`) would
install the entire repository, including both modules.  The use case for this
resolver is when you only want to install a single module contained inside a
repo, that acts as a standalone bower module.

To do this, the custom resolver matches patterns of the following form:

```
bower install <owner>/<repo>^<folder-1>^...^<folder-n>^<version>
```

So to install only `module` from above:
```
bower install githubUser/repo^namespace^module^v1.0.0
```
## Usage

1. Install this repo as a package.json dependency
    * `npm install --saveDev urbn/bower-github-subdirectory-resolver`
2. List the resolver in your `.bowerrc` file
    * `{ "resolvers": [ "bower-github-subdirectory-resolver" ] }`
3. Install your bower subdirectory
    * `bower install --save urbn/github-repo^namespace^module^v1.0.0`

Additional details can be found in the
[Bower Pluggable Resolver Docs](http://bower.io/docs/pluggable-resolvers/).

## To Be Implemented
* Properly handle checkout of specific tag before copying subdirectory (i.e.
  `namespace^module^v1.0.0`)
* Beef up error handling during checkout and copying
