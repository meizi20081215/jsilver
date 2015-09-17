# Getting Started with JSilver #

## Hello World ##
Here's a template...

`[hello-world.cs]`
```
    Hello <?cs var:name.first ?> <?cs var:name.last ?>!
```

Here's a bit of Java...

`[HelloWorld.java]`
```
    JSilver jSilver = new JSilver(new FileResourceLoader("/path/to/my/templates"));

    Data data = jSilver.createData();
    data.setValue("name.first", "Some");
    data.setValue("name.last", "Blokey");

    Writer output = ...;
    jSilver.render("hello-world.cs", data, output);
```
Here's what happens when you run it...
```
    Hello Some Blokey!
```
## A bit more detail ##

That was easy. Let's go into a teeny bit more detail.

### Templates ###
```
    Hello <?cs var:name.first ?> <?cs var:name.last ?>!
```
The template syntax is identical to ClearSilver. Anything that's valid in a ClearSilver template is valid in a JSilver template too.

Read the external ClearSilver docs on templates:

  * [ClearSilver Basics](http://www.clearsilver.net/docs/template_basics.hdf)
  * [Template Syntax](http://www.clearsilver.net/docs/man_templates.hdf)
    * [Expressions](http://www.clearsilver.net/docs/man_expressions.hdf)
    * [Macros](http://www.clearsilver.net/docs/man_macros.hdf)
    * [Functions](http://www.clearsilver.net/docs/man_filters.hdf)

### Resource Loading ###
```
   JSilver jSilver = new JSilver(new FileResourceLoader("/path/to/my/templates"));
```

JSilver needs to know where it should load templates from (especially if a template has an include of another template). It's the ResourceLoader's responsibility to load resources. JSilver comes with some out-of-the-box loaders for common situations (found in com.google.clearsilver.jsilver.resourceloaders):
| Loader | Description | Example |
|:-------|:------------|:--------|
| FileResourceLoader | Loads resources from a directory. | ` new FileResourceLoader("/path/to/my/templates") ` ||
| InMemoryResourceLoader | Loads resources from an internal map in memory | ` loader.store("some-template.cs", "Hello <?cs var:you ?>"); ` |
| ClassResourceLoader | Loads resources from alongside a class in a Jar file. | ` new ClassResourceLoader(MyClass.class) ` |
| ClassPathResourceLoader | Similar to ClassResourceLoader, but lets you specify a path within a Jar. | ` new ClassPathResourceLoader("path/in/my/jar") ` |

You may find the different loaders useful for different reasons:
  * FileResourceLoader
    * Production application where you may need access to tweak templates while the app is still running.
  * InMemoryResourceLoader
    * Small templates that can be embedded as strings in Java source code.
    * Unit tests.
    * Anywhere where you don't want to worry about the hassle of a dependency on an external path.
  * ClassResourceLoader
    * Libraries with fixed templates you intend other people to link to without them having to worry about setting additional paths.
  * ClassPathResourceLoader
    * As above.

Additionally, if you have your own application specific way of loading files (e.g. from GFS), you can always create your own implementation of ResourceLoader.

### Rendering ###
```
 jSilver.render("hello-world.cs", data, output);
```
The output argument can be a `Writer`, `PrintStream`, `System.out`/`System.err`, `StringBuilder`/`StringBuffer` or anything that implements `java.io.Appendable`.

For convenience there's also an overloaded version of the method that returns the template in a String:
```
  String out = jSilver.render("hello-world.cs", data);
```