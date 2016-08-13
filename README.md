
This is a receipe for getting Atom to work with `stack` projects
on OSX and Linux.

### Synopsis

    (edit build-ide-utils)
    $ build-ide-utils lts-6.0
    $ $HOME/atom-bin/lts-6.0/run-atom

### Setting up Atom with Haskell support

To enable IDE support (i.e. ghc-mod) for
stack projects in Atom you need to use a suite of utilties
matching the resolver of your project. This
repo contains a script to help build the
IDE utilties and invoke Atom with the correct
PATH so that they are found by Haskell IDE plug-ins.

Sections:

1. Atom Packages
2. Utility programs: `ghc-mod`, `ghc-modi`, ...
3. Testing

### Atom Packages

Install the following Atom packages:

- `ide-haskell`
- `ide-haskell-cabal`
- `haskell-ghc-mod`
- `language-haskell`

You shouldn't need to configure any of these
packages - the default settings should work.

### Utility Programs

Use the `build-resolver-bin` to build a set of utility
programs for use with a specific stack resolver.
It will also build a script to invoke Atom with
the correct PATH so these utility program will be seen.

1. Pick a resolver -- call it $RESOLVER
2. Edit the `build-ide-utils` script to configure the location
of the Atom executable.
3. Run: `build-ide-utils $RESOLVER`

This will create a script to start up Atom with the correct PATH.

Note: Utility programs built for one resolver
_may_ work with another closely related resolver, but is
advisable to use a suite of utilities tailored for the
resolver you are using.

### Starting Atom

Start Atom with:

    $ ~/atom-bin/$RESOLVER/run-atom

On OS X an `open-atom` script is availble:

    $ ~/atom-bin/$RESOLVER/open-atom

### Testing

In a new directory run:

    stack new my-project simple --resolver $RESOLVER
    cd my-project
    stack setup

and then run Atom with:

    ~/atom-bin/$RESOLVER/run-atom .

(you should be in the `my-project` directory when doing this.)

Atom should start up displaying the `my-project` directory.

Continue with:

- Click on the directory `src` in the left panel.
- Open the file `Main.hs`
- Hover the cursor over `putStrLn` - this should bring up type
information.

