---
description: Find out how to create a Command using OneConfig
---

# Command Basics

## Getting Started

To create a new Command, you need to use the `@Command(value = "commandName", decription = "description")` annotation for a class, like this:

```java
@Command(value = ExampleMod.MODID, description = "Just a simple command")
public class ExampleCommand {
```

Simple! Now, you will have a command like `/examplemod`, but the command doesn't do anything yet, lets change that. To create a function for a command, we use the `@Main` annotation, like this:

```java
    @Main
    private static void main() {
      System.out.println("Hello, World!");
    }
```

Awesome! now `/examplemod` will print in the console `"Hello, World!"`. But what about subcommands? They are easy too! We just have to make a new `class` using the `@SubCommand(value = "name", description = "description")` annotation, and then do the same thing as above, like this:

```java
    @SubCommand(value = "ping", description = "Pongs you")
    private static class pingPong{
        @Main
        private static void main() {
          System.out.println("pong");
        }
    }
```

And now, if we do `/examplemon ping`, there will be a `"pong"` printed in the console! Now, we just have to put it all together and were done!

```java
@Command(value = ExampleMod.MODID, description = "Just a simple command")
public class ExampleCommand {
    @Main
    private static void main() {
      System.out.println("Hello, World!");
    }
    
        @SubCommand(value = "ping", description = "Pongs you")
    private static class pingPong{
        @Main
        private static void main() {
          System.out.println("pong");
        }
    }
}
```

## Using Arguments

Using arguments is simple too! You just have to pass them in the function that has the `@Main` annotation, like this:

```java
        @Main
        private static void main(String arg) {
          System.out.println(arg);
        }
```

and now, we can do `/examplemod test` and the console will print out "test"
