---
description: Find out how to create a Command using OneConfig
---

# Commands

## Getting Started

To create a new Command, you need to use the `@Command(value = "commandName", decription = "description")` annotation for a class, like this:

```java
@Command(value = ExampleMod.MODID, description = "Just a simple command")
public class ExampleCommand {
```

Simple! Now, you will have a command like `/examplemod`, but the command doesn't do anything yet, lets change that. To create a function for a command, we use the `@Main` annotation, like this:

```java
    @Main
    // ps. this can't have any arguments, sorry :(
    private void main() {
      System.out.println("Hello, World!");
    }
```

Awesome! now `/examplemod` will print in the console `"Hello, World!"`.&#x20;

**But first**, we need to register our command, so OneConfig knows it exists. **Just add this to your main class's init method:**

```java
    // snip!
    CommandManager.register(new ExampleCommand());
    // some more code...
}
```

## Sub Commands

But what about sub commands? They are easy too! We just have to make a new `method` using the `@SubCommand(description = "description")` annotation, and then do the same thing as above, like this:

```java
    // can be static or nonstatic
    @SubCommand(description = "Pongs you", aliases = {"p", "pp"}) // p.s. the args are optional!
    private void ping(String anArg) {
        UChat.chat("Pong!");
        // this command can be accessed by either the method name, or its aliases; e.g:
        // /examplemod ping <arg>, /examplemod p <arg>, /examplemod pp <arg>
        System.out.println("I called with arguement " + anArg);
    }
```



## Sub Command Groups

Imagine a place where you could have sub commands in groups, like `/hello ping pong` and `/hello ping pingpong`. Well, you can! Just create a new nested or inner class, like this:

```java
@Command(value = ExampleMod.MODID, description = "Just a simple command")
public class ExampleCommand {
    // snip!
    
    
    // this specifies the name of the subcommand group, like the @Command annotation
    // specifies the name of the command.
    // with this one, a use could do /examplemod ping, /examplemod pingg, or /examplemod pingu to access this.
    @SubCommandGroup(value = "ping", aliases = {"pingg", "pingu"})
    // can be static, nonstatic
    private class ASubCommandGroup {
        // subcommand groups can have a @main as well!
        // this is called when a user types /examplemod ping 
        @Main
        private void method() {
            UChat.chat("pong!");
        }
        
        @SubCommand()
        private void hi() {
            // accessed with /examplemod ping hi
            System.out.println("hello");
        }
    }
    
}
```

## Using Arguments

Using arguments is simple too! You just add them as normal arguments to a method, like normal Java. Here are some examples demonstrating features of the arguments:

```java
        // snip~
        
        // greedy example
        @SubCommand()
        private void whatDidISay(@Greedy String s) {
            // @Greedy means it will consume itself and all arguements after it.
            // It has to be the last argument on a method (for odvious reasons)
            // so someone could write whatever they want after it. 
            // /examplemod whatDidISay hello I said this cool thing
            UChat.chat("You said: " + s);
        }
        
        // basic example
        @Subcommand(aliases = {"minus"})
        private void subtract(int something, int somethingelse) {
            UChat.chat(something - somethingelse);
        }
        
        // descriptions! (optional, but recommended)
        @SubCommand(description = "Add two numbers.")
        private void add(@Descripton("First number") int a, @Description("Second number") int b) {
            // woah, whats this @Description?
            // @Description allows you to add information about the param to the user in the help message.
            // so, with these descriptors, if a person called /examplemod help:
            
            // Help for /examplemod:
            // (other command help and stuff)
            // /examplemod ping add <First number> <Second number>: Add two numbers.
            
            // would be displayed. Anyways, back to the code.
            UChat.chat("Sum is: " + (a + b));
        }
        
        // autocomplete!
        @SubCommand()
        private void autocompleteDemo(@Descripton(autocompletesTo = {"PLAYER"} String s) {
            System.out.println(s);
            // this command autocompletes to player names in the server right now (cool)
        }
        
        @SubCommand()
        private void anotherDemo(@Descripton(autocompletesTo = {"maybe", "call", "me"} String s) {
            System.out.println(s);
            // this command autocompletes to the list of args given above. ^
            // booleans also have automatic autocompletion for their args :)
        }
```

So, this quick demo hopefully has enlightened you on all the OneConfig command system has to offer. It has a much nicer syntax than brigadier or legacy command handling, and is (almost) just as feature rich! Here is a quick recap:

* Any method will be added as its name if annotated with `@SubCommand`
* Classes or methods can be of any visibility, and static or non-static
* Must be registered using `CommandManager.register(new MyCommand());`
* Descriptions and aliases are displayed in help messages, and it is recommended you describe what each command does, and its arguments, even if it is just naming them.
