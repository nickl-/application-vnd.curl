# Curl { } 
### media type: application/vnd.curl

Found these scattered all over sourceforge and thought we might benefit from having them mirrored and 
combined in a single location here on github where we can colaborate together. If this also finds your 
intrigue lets run it through it's paces and see what it can do.

Busy with yet another **RESTful API** implementation **hax**, still looking for that missing **HATEOAS** glove 
that fits as I am sure many of you are too. **(X)HTML** is still the only hypermedia type that can at least
manage both form input as well as links but without the missing idempotent methods **HEAD**, **PUT**, 
**DELETE** and no concern to Accept: anything other than what it receives, with no hope that this will
change anytime soon. 

The few that are considering the inevitable move to go and actually register a media type for this purpose
all seem to fall short in one way or the other, I won't point fingers or they don't seems to get the support 
they need. Can you believe **JSON-Schema** is completely off track now, I ask you?

## Purpose
I see this as research space, where we can try these tools and specification on for size, translate some of
the documentation and write some additional libs. Show off what we can do and help each other out where it
just doesn't want to. If it works, bonus we have a hypermedia type, one that goes way beyond the requirements
and beyand my wildest dreams at least. 

Let me not get ahead of myself join me on a journey of discovery...

## Abstract
The work described here explores the design of **Curl**, a single, coherent linguistic basis for expression of Web 
content at levels ranging from simple formatted text to contemporary object-oriented programming. **Curl** is part 
of a research effort aimed at eliminating discontinuities from the function/sophistication curve. This yields an 
authoring environment in which; 
 1. incremental functionality requires incremental skill acquisition, and 
 2. a consistent semantics avoids communication obstacles between separately encapsulated fragments of content. 

## Introduction

**Curl** is a new language for creating web documents with almost any sort of content, from simple formatted text 
to complex interactive applets.

 * Text formatting,
 * Scripting simple interactions.
 * Programming complex operations.

**Curl** is intended to be a ***gentle slope*** system, accessible to content creators at all skill levels ranging 
from authors new to the web to experienced programmers. By using a simple, uniform language syntax and semantics, 
**Curl** avoids the discontinuities experienced by current web users who have to juggle **HTML**, **JavaScript**, 
**Java**, **Perl**, etc. to create today's exciting sites. Our hope is that the single environment provided by **Curl**
will be an attractive alternative for web developers.

## Overview

The name **Curl** derives from it's principle syntatic sugar: **Curl's** source consists of arbitrary text, punctuated 
by expression and enclosed in curly braces **{ }**. Just like in **HTML** plain text denotes to valid source but unlike 
in **HTML** the escapes extend to a real object orientated programming language. 

Lets see some **Curl**:

Curl source (markup)

```curl
The following characters are displayed using a {bold bold-faced font}. There are {+ 10 4} bold characters altogether.
```

User presented output

```
The following characters are displayed using a bold-faced font. There are 14 bold characters altogether.
```

What is so fancy about that you might say? Can your markup do this:

```
{let color:Dynamic='red
     count=0    | "quantity" can't depend on itself
     quantity:Dynamic=count
  {vbox
    {title Beach Balls}
    {hbox "Color:"
          {radiobuttons foo 'red 'white 'blue
            action={color.set-value foo}}}
    {hbox "Quantity:"
          {button "Take another"
            action={quantity.set-value
                     {set count {+ count 1}}}}
          {button "Give one back"
            action={when {> count 0}
                     {quantity.set-value
                       {set count {- count 1}}}}}
    {paragraph You've ordered {value quantity}
               {value color} beach balls!}}}
```

Producing a dynamic input form:

 <img src="http://groups.csail.mit.edu/cag/curl/beach1.gif" title="A very 2006 looking form">

Or Lets Parse a JSON Value As A JSON Object:
JSON 
```json
{ 
  "id": one hundred twenty-three, 
  "Okada": "name", 
  "Tokyo": "address", 
  "hobbies": ["Snowboard", "Golf"]
}
```
Curl
```
let obj: JsonObject = 
    {JsonValue-Parse {url "Test.Json"}} ASA JsonObject 
    dump { 
        v ["id"], 
        v ["name"], 
        v ["address"], 
        v ["hobbies"] [ 0], 
        v ["hobbies"] [an] 
    }
```

A simple Curl applet for HelloWorld might be
```
     {Curl 5.0, 6.0, 7.0 applet}
         {text
          color = "blue",
          font-size = 16pt,
          Hello World
     }
```

**Curl** provides both macros and text-procedures in addition to anonymous procedures and named methods. An alternative 
using the text-procedure paragraph would be:
```
     {paragraph
          paragraph-left-indent=0.5in,
          {text color = "red", font-size = 12pt,
               Hello
          }
          {text color = "green", font-size = 12pt,
                    World
          }
     }
```
Recently this style of layout has been adopted by "builders" in the Groovy language for the JVM, but is also familiar to users of CSS or Tcl/Tk. Most features for web applications now implemented through combinations of JavaScript libraries + HTML + CSS are already found within the Curl language, including features usually associated with Prototype + script.aculo.us such as accordion panes.
Curl sets callbacks in the manner also adopted by Groovy:
```
     {CommandButton width=100pt,
          height = 50pt,
          label = {center {bold Invokes an event handler when clicked}},
          control-color = "orange",
          || Attach the following event handler to this CommandButton
          {on Action do
               {popup-message
                    title = "Your Message",
                    "This is a user message dialog."
               }
          }
     }
```
Obvious influences on **Curl's** design include **LISP**, **C++**, **Tcl/Tk**, **TeX**. Language design 
decisions directly reflect the goal of reconciling its simple accessibility to naive users with the power and 
efficiency demanded by sophisticated programming tasks. 

Salient features of **Curl** include:

### Programs as documents
Execution of every **Curl** program results in a document containing a set of objects that may be displayed or 
otherwise manipulated. **Curl** includes an extensible GUI which provides for simple, structured arrangement of 
displayable objects. Curl objects appear self aware having their meta data available as well as the instructions
to present itself. 

### Syntax and Semantics
 * **Extensibility.** Arbitrary sub-languages can be embedded as new *{...}* forms and be processed correctly 
through simple extension of the environment. 

For example, the following Curl form

```
     {circuit-simulation-netlist
          M1 out in gnd gnd nmos w=4u l=1u
          M2 out in vdd vdd pmos w=8u l=1u
          VDD vdd gnd 5v
          VIN in gnd pwl(0 0 0.1 5)
          .tran .1n 10n
          .plot v(in) v(out)
     }
```

might be found in a document for an engineering course where the instructor wished to insert an interactive simulation 
for the student to explore. 

 * **Strong typing.** Every variable and value may be declared and type-checked at compile time. 

 * **Ambiguous types.** In the absence of declarations, variables default to type **any**. The semantics of a **Curl** 
program are unchanged if all type declarations are eliminated, although its performance will suffer. 
This is the flip side of strong typing: providing types for each argument or variable can be a time consuming process 
which may not be worthwhile while prototyping new ideas or when efficiency is not of concern to the author.

 * **Lexically-scoped environment.** **Curl** provides a structured name space whose bindings include variables, 
constants, types, and compilation hooks for arbitrary syntactic forms. The name space is instantiated as an environment
which spans compile and run times, and which completely dictates the semantics which will be associated with source code
during compilation. 

 * **Procedural semantics.** Procedures are first-class data, implemented using closures as necessary. Positional and 
keyword arguments are supported.

 * **Objects.** Types include classes, with multiple inheritance, arrays, and primitive types such as integers.

 * **First-class types.** Types, including classes, are first-class objects: they are bound in the environment, and obey
consistent scoping rules; they may be arguments to or results from arbitrary computation both at compile and run times. 
Having type information available at run time allows programs to examine and manipulate arbitrary objects without without 
the need of out bound information.

### Portability, Performance and Safety
 * **Efficient native representations.** Representation conventions for values with declared types are tag-less, consistent 
with **C** and **C++**, yielding similar code efficiency.
 * **Incremental compilation.** Local compilation of source code to native code is the basis of Curl portability, safety, 
program encapsulation and performance. Code that has been compiled may be cached locally in memory or on disk.

### Other Features
 * **Threads.** **Curl** supports a simple platform-independent thread model. Threads are particularly useful in the 
"real-time" environment of the Web where the use of blocking input/output can lead to extremely frustrating delays when 
accessing foreign data.
 * **Garbage Collection.** By default, Curl objects are garbage collected when they are no longer used.

## Types

Efficient implementation on contemporary processors, as well as easy interfacing to foreign software environments, 
dictates the use of conventional **C/C++** representations of data. To provide typeless simplicity for simple 
scripting-level programming, **Curl** provides the ambiguous type any which may require the run-time representation of 
type information. Thus
```
      {let a:any=5
          {define {f x:int}:int {return {+ x 3}}
               {f a}
          }
      }
```
will be compiled so that the ambiguously declared variable a carries a run-time type, while the formal parameter x to 
the integer procedure f does not. Passing a to f requires a cast, which involves a run-time type check after which the 
value portion of a is passed as an integer. To perform such casts efficiently, type information (when present) is 
separated from the representation of values. Because the storage for a value of type any is allocated by the compiler, 
casting a value to the ambiguous type never causes dynamic storage allocation.

Note that the omission of a type declaration for a variable means something different than in, for example, **ML**. In 
**ML** the variable has a static type that the compiler must determine. In **Curl**, an omitted type is an under-specification 
and the actual type may change during program execution.

Since run-time representations are required for our extensible system of types, it is convenient to represent them as 
**Curl** objects and to expose them in the programming model. Thus **Curl** types are simply values: they are named, 
passed, stored, and accessed identically to other **Curl** data. This treatment of types provides a natural and 
consistent semantics for type extension, for type portability (which reduces to the problem of object portability), 
and for extended type semantics. For example, in

```
     {let t1:type={array int}
          t2:type={list-of t1}
          x:t2
     ...}
```
array and list-of are procedures which generate types. This emancipation of types, while semantically appealing, 
presents certain challenges. It requires that compilation order be somewhat lazy, to accommodate circularities. 
Moreover, the expressibility of mutable type variables admits constructs whose efficient translation, or even whose 
meaning, is questionable. We currently forbid such constructs, requiring that types used in declarations be evaluable 
to compile-time constants.

Ambiguous types, as well as the object class hierarchy, yield a type lattice in which a value may have arbitrarily 
many types, only some of which are compile-time constants. The run-time type of a value v may be explored using 
```{typeof v}```, which returns the most specific type object appropriate to v, using run-time tags if necessary. 
Similarly, ```{isa t v}``` tests the membership of v in type t, again using the fully-disambiguated run-time type of v.

## Objects

Modern programming practice demands support for objects, and their advantages are particularly compelling in the context
of an extensible Web programming environment. Objects provide a natural implementation for the hierarchy of displayed 
images on a Web page, and they support incremental extension of previously defined behavior. In its pure form, however, 
an object-oriented programming model fails to meet the "gentle-slope" goal: the naive user cannot simply add a variable 
to his otherwise textual Web page, for example. A consequent subgoal of **Curl** is the graceful integration of object
semantics into a lexically-scoped procedural programming model.

Most **Curl** types are classes. In the abstract, a **Curl** class provides a namespace whose scope includes objects of 
that class. Within a class, names can be bound to values, both variable and constant; the latter includes methods 
specific to the class. Instances of a class have a run-time representation containing slots for the values of variable 
data, as well as dispatch tables for efficiently invoking methods of the class. Our current implementation uses 
representations similar to those of *C++**.

## Graphic Objects

**Curl's** object-oriented graphical user interface combines both high-level interfaces with the usual repertoire of low-level primitives. A graphic image is represented as a hierarchical tree of Graphic objects. Leaves of the tree are primitive Graphic objects which know how to draw themselves, usually after looking up the values of various properties (see below). Primitive Graphic objects include:
 * **lines and curves.** Properties control the color, width, dash style and end treatment (e.g., none, arrowhead, ball, ...).
 * **rectangles, polygons, ellipses.** Properties control the width and color of the border, and the stipple and color of the fill. Various 3-D effects are also provided for the borders of rectangles.
 * **text.** Properties control the color, size and font family as well as indicating whether the text should be bold or italic.
 * **multi-line text.** Similar to text, but can display itself across multiple lines.
 * **color bitmaps.** *Curl* supports the usual collection of image formats (**GIF**, **JPEG**, ...).
 * **glue.** Glue has no visible representation but provides some parameterized dimensional flexibility that is useful in the formatting operations provided by Boxes (see below).

The basic graphic building block is the Box which serves as the parent to a collection of primitive Graphic objects and instances of other Boxes. The displayable hierarchy consists of a tree (or graph) of such objects.
In addition to providing the abstraction mechanism for building complex images, various types of Boxes also control the positioning of their children using dimension information the children supply. Current formatting templates include:

 * **hboxes and vboxes.** These are one-dimensional formatters that create simple horizontal or vertical arrangements of their children, lining up their baselines or margins. As in TeX, the relative allocation of white space is controlled by the elasticity of any glue objects that have been added as children.
 * **tables.** A two-dimensional formatter that aligns the margins and baselines of its children on a Cartesian grid. The row and column of each child is specified as it is added to the table template; a child can span multiple rows and/or columns.
 * **paragraphs.** Children are positioned left-to-right top-to-bottom. Children on the same line have their baselines aligned and the inter-line spacing is chosen to accommodate the tallest child on a line.
 * **canvases.** No explicit formatting is provided; each child is given a position as it's added to the canvas template.

This set of formatting primitives is sufficient to duplicate the effects of most text formatters and browsers with little effort on the part of the Curl user.



That should be enough to wet the taste-buds, if you like... if you dont? Lets hear about it the issue queue will be open and feel free to write in the wiki. 




### Sources
http://groups.csail.mit.edu/cag/curl/wwwpaper.html<br>
http://en.wikipedia.org/wiki/Curl_(programming_language)<br>
http://developers.curlap.com/re-reference/25-data/7-json.html<br>

## Wall of fame - commiters @ sourceforge
dmccrae        = [Doug McCrae](dmccrae@users.sourceforge.net)<br>
ihokada        = [Hitoshi Okada](hokada@users.sourceforge.net)<br>
mgordon-curl   = [Michael Gordon](mgordon-curl@users.sourceforge.net)<br>
wbardwel       = [William Bardwell](wbardwel@users.sourceforge.net)<br>


### Copyright & Acknowledgement - where it's due
Copyright © 1998-2008 [Sumisho Computer Systems Corp.](http://www.curl.com/company/)<br>
Invented @ [MIT Computer Science and Artificial Intelligence Laboratory](http://groups.csail.mit.edu/cag/curl)

### With a warm and fuzzy license
Apache License<br>
Version 2.0, January 2004<br>
http://www.apache.org/licenses/
