# dotconv

A tool to convert code into a GraphViz dot flowchart.

## Building/running

> [!WARNING] 
> Project is in early development, expect many breakages and bugs

Use the meson build system:
```
meson setup build
meson compile -C build
```

## Supported languages
 - C++
 - More planned

## Purpose/Motivations

This tool is developed with the idea of automating flowcharts of code
algorithms. LLVM has the `opt` tool however it only creates control-flow
diagrams of LLVM IR language, not C++. It's hard to piece together the original
intent of the code when in IR form, which is why this tool exists; it provides
an easy way to create flowcharts from code.

This tool's original motivations derive from documenting algorithms in A-level
computer science coursework. The design part requires flowcharts and other
diagrams to get higher marks, however most of the time algorithms end up being
done while the code is being written. Creating flowcharts is time-consuming, and
this tool should speed it up for anyone wanting to create one from code. Of
course, you still have to translate the code into english in the flowchart :P

## Design

dotconv is essentially just a compiler, except instead of translating to machine
code, only control statements such as loops and if/switch statements are
"compiled". This in effect models all the different paths that the code can
take in the flowchart.

The flowchart will just be represented by a "dot" file. This is a way to
represent flowcharts in a language, which uses nodes and edges as relationships.
Labels can be added to them to add text to the nodes/edges to describe them. The
code will be used as labels in this case, including the output of if statements
and the like.

This will require tokenising the input file, then putting each line of code as a
label for a new node. These can be joined with '->'. Each node can be defined
with a label and potentially other attributes such as shape, colour etc, and once
all the nodes are scanned, the relationships can then be calculated and added to
the .dot file.

## Planned features and status
 - [ ] Multiple language support

## Resources
 * [LLVM's opt](https://llvm.org/docs/Passes.html#dot-cfg-print-cfg-of-function-to-dot-file)
