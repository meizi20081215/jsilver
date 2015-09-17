JSilver is a pure-Java implementation of [Clearsilver](http://www.clearsilver.net/). Key benefits of JSilver over Clearsilver include:
  * Performance
    * Templates are only parsed when the file changes - not for each request.
    * Optionally, templates can be compiled directly to Java bytecode, making rendering super-fast.
    * Once-off template optimization step simplifies template making rendering even faster.
    * Internal optimizations to streamline string manipulation.
  * Avoids the complexities of JNI
    * Avoids the risk of native code taking down the JVM.
    * Avoids JNI marshalling overhead.
    * Simplifies IDE use (no more forgetting java.library.path).
  * Allows for easy extension in Java
    * API allows template functions to be defined in Java allowing logic to be pulled out of templates.
    * Custom escaping / text filters can be plugged in.
    * Makes plugging in translations much simpler (e.g. <?cs var:translate('some.message') ?>).
    * API designed with testability in mind.
    * Custom mechanisms can be plugged in for loading templates and caching.
    * Low-level access to template AST for advanced transformations.

See the [Getting Started guide](GettingStarted.md).