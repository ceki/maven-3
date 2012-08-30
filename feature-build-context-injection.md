Automatic BuildContext injection and lifecycle management

igorf 2012-08-29
I think far better idea is to introduce general purpose mojo execution
scope and callbacks to allow maven extensions to manage contribution
and cleanup of components to the scope. This will cleanly solve current
problem with circular dependency between tesla and build-avoidance
source trees and I am sure mojo execution context will be useful for
other things
==== 


New BuildContext instance is automatically created and associated with each
project mojo execution and can be injected as a plexus or jsr330 component
to the mojo itself or any of components directly or indirected used by the
mojo.

BuildContex is automatically closed after mojo execution and execution failure
exception is raised if there are uncleared error messages reported to the 
build context.

Digested information about maven plugin artifact and all its dependencies is
automatically stored in the build context and full build is triggered if any
of the artifact changes. Likewise, project effective pom and session execution
properties are stored in the build context and changes to either will result
in full build.

Open questions

* either cleanup tesla-build-avoidance API and implementation or define 
  separate tesla-specific and hopefully easier to understand and use 
  BuildContext interface
