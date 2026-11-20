This is an official list of implementations for SIMAS, the **Sim**ple **As**sembly programming language. <br><br>
Want to make your own implementation? Check out the [official specifications](https://GitHub.com/turrnutorg/SIMAS-spec)

# Known Implementations

## Objective-CMAS
### "Best" version
#### Objective-CMAS-GUI (current version)
SIMAS brought to Objective-C. Low-level performance with a highly extensible architecture, compatible with nearly all computers running Mac OS X; now with a GUI!<br>
[Objective-CMAS-GUI](https://www.github.com/tuvalutorture/objective-cmas-gui)
#### Objective-CMAS (original)
SIMAS brought to Objective C. Low level performance with an extensible architecture and compatibility. Archived in favour of Objective-CMAS GUI<br>
[Objective-CMAS](https://www.github.com/tuvalutorture/objective-cmas)

## SIMASJS
### original version
The original implementation for SIMAS, written in JavaScript. Good for general purpose or web development.<br>
[SIMASJS](https://www.github.com/turrnut/simas)

## CMAS
SIMAS Interpreter written in The C Programming Language. Used for low level programming; largely replaced by Objective-CMAS. <br>
[CMAS](https://www.github.com/turrnutorg/CMAS)

# Strengths & Weaknesses of each version
With anything that has variants, there will inevitably be things some are better at than others.<br>
SIMAS, being a language with multiple implementations in multiple languages, is no different. <br>
This section covers the differences between the language implementations, and why you may want to use one over the other.<br>

## SIMASJS
SIMASJS features many unique features which programmers may find helpful; however, it is not without glaring flaws.
### Strengths
* SIMASJS features *aliased* operations---that is, operations like `AND` can instead be substituted for `+`.
* SIMASJS features a dedicated instruction to spin up a web server, a feature not present anywhere else.
* SIMASJS is written in JavaScript, meaning it is easily incorporated into other JavaScript/web projects with relative ease.
* SIMASJS allows string literals to remain unquoted without issue.
* SIMASJS cannot leak memory, as it is inherently managed by the JS runtime.
### Weaknesses
* SIMASJS lacks function call nesting, as in, a function call inside of a function is almost guaranteed to break the interpreter.
* SIMASJS requires extra steps to run programs (a compilation step and an execution step), which may feel clunky.
* SIMASJS's architecture is quite unextensible; for you cannot add new instructions to the language without modifying the language's code itself.
* SIMASJS may reveal itself to be quite heavy to run, as it relies on the JavaScript language, compared to lighter-running languages.
* SIMASJS is the least compatible incarnation of the language, as later re-implementations change fundamental things about certain language features / instruction behaviours.

## CMAS
CMAS is a "second incarnation" of SIMAS, bringing many new changes, while breaking things along the way and being a wee bit prone to dying.
### Strengths
* CMAS is quite fast and lightweight, even being able to run on MS-DOS (no, really! it compiled and ran on Borland Turbo C on the "medium" memory model!) without issue.
* CMAS supports calling functions within functions.
* CMAS is *extremely* portable, being written entirely in ANSI C (C89/C90), a standard supported by *virtually* every C compiler ever written.
* CMAS's parser and architecture is much less fragile, and is technically extensible via function pointer registration.
### Weaknesses
* CMAS is fairly unstable, often leading to outright crashes or segmentation faults if fed malformed inputs. 
* CMAS's parser, while more robust than SIMASJS, is still quite fragile, and quite heap-intensive.
* CMAS has *no* argument validation at parse-time, meaning malformed inputs may sneak through into the runtime and wreak havoc.
* CMAS, while technically extensible, realistically still has no way of extending the language outside of the runtime.

## Objective-CMAS (base)
Objective-CMAS is, arguably, the *objective*-ly (hah, get it? i'm so funny lmao omg im so quirky, kill me now) best implementation of SIMAS. <br>
### Strengths
* Objective-CMAS is very extensible, supporting dynamic bundle loading at runtime, and those libraries can add new types and instructions to the language without modifying the core language.
* Objective-CMAS's .xcodeproj features a dedicated dylib target, allowing you to load the runtime into any objective-c application and incorporate its features.
* Objective-CMAS features a vastly more robust type system designed to be extensible and retain your data.
* Objective-CMAS is built with Objective-C 1.0, meaning you can compile it on anything from your iBook G3 to your modern M5 Max PROLED MacBook Pro.
* Objective-CMAS is much more resilient to runtime issues, often gracefully exiting rather than full-on crashing.
* Objective-CMAS inherits all instructions from CMAS, while extending them.
### Weaknesses
* Objective-CMAS, by nature of the language it's written in, is largely bound to the Mac OS X ecosystem (though I do not doubt it would compile on a compatible system like GNUStep).
* Objective-CMAS can cause memory leaks (manual reference counting is easy, but i try my best to not eated your rammies o7).
* Objective-CMAS is inherently slower due to the overhead of Objective-C messaging.
* Objective-CMAS is also *heavier* because of the messaging.
* Objective-CMAS's code, for those looking to extend/build upon it, is quite... dense.
* Objective-CMAS is deprecated in favour of Objective-CMAS-GUI.

## Objective-CMAS (GUI)
Objective-CMAS-GUI (referred to here as just Objective-CMAS for the sake of brevity), counterintuitively, brings real improvements besides just a fancy UI, believe it or not.
### Strengths
* Objective-CMAS, of course, is now given a GUI interface to interact with your code.
* Objective-CMAS's GUI features things such as a (though basic) stepper.
* Objective-CMAS's runtime is now thread-safe, moving away from static singletons to per-thread instantiation.
* Objective-CMAS now features *parse-time argument validation*, meaning you can't get away with putting a string constant where a variable name should go.
* Objective-CMAS, for the first time in SIMAS history, has *scoping*. Labels and variables are now scoped within blocks, the main type being functions (so now any temp vars in a function won't pollute the global namespace).
* Objective-CMAS is even more robust and memory safe.
* Objective-CMAS supports structures, allowing you to organise variables into object-like containers.
### Weaknesses
* (almost) All of the above from base Objective-CMAS.
* The GUI target requires Mac OS X 10.6's features, the XIB file requires macOS 10.14 Mojave running Xcode 10 to open, and requires additional work to compile it on lower Xcode versions (i.e. adding explicit `@synthesize` directives in Xcodes <4 because the code relies on auto-synthesis).
* The GUI Highlighting feature is, admittedly, broken upon file imports (uhhh whoops, sorry, i'll fix that :P).
* The GUI acts as a basic text editor rather than a proper IDE.
