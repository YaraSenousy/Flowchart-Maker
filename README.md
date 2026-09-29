# Flowchart Maker

A Windows desktop app for drawing and validating flowcharts, written in C++ on the CMU graphics library, for a Programming Techniques course. Users build a flowchart from statement blocks, connect them, save and load it, and switch to simulation mode to validate it.

## Features

**Design mode**
- **Statements:** Start, End, value assignment (`x = 5`), variable assignment (`x = y`), operator assignment (`x = y + z`), condition (for if-statements and loops), Read, and Write.
- **Connectors** between statements, with each statement tracking its outgoing connection.
- **Editing:** select, copy, paste and delete statements.
- **Files:** save the whole flowchart to a text file and load it back (`save.txt` is an example).

**Simulation mode**
- **Validate** checks that the chart has exactly one Start and one End and that every statement has an outgoing connector, reporting the first problem in the status bar.

Edit, Cut and Run have toolbar icons but aren't implemented yet.

## Design

![Class diagram](ClassDiagram.jpg)

- **`ApplicationManager`** owns the statement and connector lists and the `Input`/`Output` GUI wrappers. It maps each toolbar click to an action.
- **Actions** use the Command pattern: every user operation (`AddStart`, `AddCond`, `AddConn`, `Copy`, `paste`, `DelAction`, `SaveAction`, `LoadAction`, `validate`, …) is an `Action` subclass with `ReadActionParameters()` and `Execute()`.
- **Statements** derive from an abstract `Statement` base class (`Start`, `End`, `ValueAssign`, `VariableAssign`, `OperatorAssign`, `Condition`, `Read`, `Write`), and each knows how to draw, save and load itself.
- **GUI:** `GUI/Input` and `GUI/Output` wrap the CMU graphics window (toolbars, drawing area, status bar). The toolbar icons live in `images/`.

## Building

This needs Windows and Visual Studio: open `PT Project.sln` and build. The CMU graphics library it uses (`CMUgraphicsLib/`, included) is Win32-only.
