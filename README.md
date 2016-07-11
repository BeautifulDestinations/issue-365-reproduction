Small test case for recreating https://github.com/commercialhaskell/stack/issues/2365

With a clean ~/.stack, ~/.ghc, ~/.ghcjs, run:

```
  cd project-b
  stack setup && stack build
  # much ghcjs-related building happens now
  find ~/.stack/ ~/.ghc ~/.ghcjs > filelist-intermediate.txt
  cd project-a
  stack setup && stack build
```

The output of the last step is:

```
benc@ghcjs-env-ba78:~/src/bd-365/project-a$ stack setup && stack build
stack will use a locally installed GHCJS
For more information on paths, see 'stack path' and 'stack exec env'
To use this GHCJS and packages outside of a project, consider using:
stack ghc, stack ghci, stack runghc, or stack exec
Ignoring that the GHCJS boot package "aeson" has a different version, 0.9.0.1, than the resolver's wanted version, 0.8.0.2
Ignoring that the GHCJS boot package "attoparsec" has a different version, 0.13.0.1, than the resolver's wanted version, 0.12.1.6
Ignoring that the GHCJS boot package "scientific" has a different version, 0.3.3.8, than the resolver's wanted version, 0.3.4.4
Ignoring that the GHCJS boot package "case-insensitive" has a different version, 1.2.0.4, than the resolver's wanted version, 1.2.0.5
Ignoring that the GHCJS boot package "hashable" has a different version, 1.2.3.2, than the resolver's wanted version, 1.2.3.3
Ignoring that the GHCJS boot package "async" has a different version, 2.0.1.6, than the resolver's wanted version, 2.0.2
Ignoring that the GHCJS boot package "vector" has a different version, 0.11.0.0, than the resolver's wanted version, 0.10.12.3
Ignoring that the GHCJS boot package "text" has a different version, 1.2.1.1, than the resolver's wanted version, 1.2.2.0
Ignoring that the GHCJS boot package "stm" has a different version, 2.4.4, than the resolver's wanted version, 2.4.4.1
Ignoring that the GHCJS boot package "dlist" has a different version, 0.7.1.1, than the resolver's wanted version, 0.7.1.2
Ignoring that the GHCJS boot package "pretty" has a different version, 1.1.3.2, than the resolver's wanted version, 1.1.2.0
Ignoring that the GHCJS boot package "containers" has a different version, 0.5.6.3, than the resolver's wanted version, 0.5.6.2
Ignoring that the GHCJS boot package "transformers" has a different version, 0.4.3.0, than the resolver's wanted version, 0.4.2.0
project-a-0.1.0.0: unregistering
byteable-0.1.1: using precompiled package
Progress: 1/2Running /home/benc/.stack/programs/x86_64-linux/ghcjs-0.2.0.20151230.3_ghc-7.10.2/bin/ghcjs-pkg --user --no-user-package-db --package-db /home/benc/.stack/snapshots/x86_64-linux/lts-3.20/ghcjs-0.2.0.20151230.3_ghc-7.10.2/pkgdb describe --simple-output byteable --expand-pkgroot exited with ExitFailure 1


ghcjs-pkg-0.2.0.20151230.3-7.10.2: cannot find package byteable
```

This does not seem specific to byteable. For example, I've encountered it with data-default.
