# CURL - media type: application/vnd.curl


## Abstract.
The work described here explores the design of Curl, a single, coherent linguistic basis for expression of Web content at levels ranging from simple formatted text to contemporary object-oriented programming. Curl is part of a research effort aimed at eliminating discontinuities from the function/sophistication curve. This yields an authoring environment in which (1) incremental functionality requires incremental skill acquisition, and (2) a consistent semantics avoids communication obstacles between separately encapsulated fragments of content. We characterize Curl as a "gentle slope system" because it makes it easy to transition from one point to another in the function/sophistication spectrum.


## Introduction

Curl is a new language for creating web documents with almost any sort of content, from simple formatted to text to complex interactive applets.

 * Text formatting,
 * Scripting simple interactions.
 * Programming complex operations.

## Overview

The name **Curl** derives from it's principle syntatic sugar: Curl's source files are arbitrary text, punctuated by expression and enclosed in curly braces ***{}***. Just as in HTML plain text denotes valid source but unlike HTML the escapes extend to a real object orientated programming language. Lets see some Curl:

Curl source (markup)

```curl
The following characters are displayed using a {bold bold-faced font}. There are {+ 10 4} bold characters altogether.
```

User presented output

```
The following characters are displayed using a bold-faced font. There are 14 bold characters altogether.
```

More Curl sugar you say?

```curl
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

And wallah:


