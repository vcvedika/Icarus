# Icarus

Icarus is a `REPL` that implements all the standard Relational Algebra Operations in CPP. Relational algebra is a procedural query language, which operates on relations (tables which are modelled using CSV files in this project) using some specified operators, such as `select`, `project`, `cartesian product`, `join`, `division`, `rename` etc. to answer user-defined queries. We use in memory storage to process all the queries, and also allow users to save the results.

The following relational algebra operations have been implemented:

- [Projection](#project)
- [Rename](#rename)

These constitue a complete set of relational algebra operations, meaning that all other operations can be realized with the help of the composition of the same.

## Supported REPL Commands

All the commands as well names `ARE` case-sensitive in nature. All the reserved keywords would be in `UPPERCASE`.

### Non Nestable Commands

These commands are non-nestable in nature, that is they must be executed on the fresh line of the REPL and cannot be merged or used with conjunction with any other commands.

- `HI`: Asks Icarus to introduce itself. A short sanity check!
- `EXIT`: Exits out of the REPL.
- `LOAD <path_to_csv_file>`: Reads the provided CSV file and stores it as a table, which can be referred to by it's name in the subsequent REPL commands. The CSV files are expected to have headers, and use `,` as their delimeter. The name of the CSV file is used as the relation name by default.
- `SHOW TABLES`: Gives a brief description of the database, with all the loaded tables, and their field and row counts.
- `SHOW <table_name>`: Shows the records from the table that has been input by the user.

### Nestable Commands

These are the basic operators of Relation Algebra which can be nested to create complex queries. Some notes that must be kept in mind while using the same:

- All the operations are CASE-SENSITIVE, for the names and commands both.
- The REPL has an inbuilt memory, so all the data that can be populated before the execution of the said command will be remembered.
- Table names can also have lowercase alphabets as uppercase strings are reserved for keywords.
- The commands are whitespace agnostic.

Here is a detailed documentation related to the syntax of the same:

#### Project

- `Syntax`: `PROJECT(table, fieldName1, fieldName2, ...)`
- `Use`: Displays all the specificied fields from the table identified by `table`. The `table` field can be either a name of the table in the database, or another relational operator which returns a table.
- `Sample Usage`: `PROJECT(courses, CourseID)`

#### Rename

- `Syntax`: `REANME(oldTableName, newTableName)`
- `Use`: Renames an already existing table identified by `oldTableName` to `newTableName` for convinience. `oldTableName` also accepts an already existing table in the memory.
- `Sample Usage`: `RENAME(students, stud)`

## Available Methods for Scripting

These functions are exported on the `Icarus` class, that can be used by the programmer to customize the behaviour of Icarus and interact with the engine programmatically.

- `startREPL`: This is the main method which starts the interactive session with the user.
- `setFieldWidth`: Takes an `int` as argument with is used to set the width of columns outputted in the `SHOW TABLES` command. Defaults to `40`
- `loadCSV`: Used to load a CSV to the database before starting the REPL. Takes in a `const &string` as the argument, denoting the path to the file. Equivalent to calling the `LOAD` command in the REPL. Returns `""` if the parsing resulted in some error, or with the table name that was formed. May require command line iteration.
- `execute`: Takes in a string as input. Executes the same as a raw command that may have been entered in the REPL. Used as a way to programatically work with the Icarus engine from your programs.

## Running the CLI

The project uses `make` to bundle the dependencies and make a working executable.

To make an excutable of the [`main.cpp`](./main.cpp) file, you can use the `make compile` command in the terminal. To directly compile and run the program, you can use `make run` command, which first uses the `compile` command to make the executable and then tries to run it in the shell.

## Features

- Built using the `OOPS` paradigm, which all of the data of a particular class being private by default and then only being exposed by the means of getters, setters and utlity functions.
- `Tables`
  - Utilities to view the table and it's content in the command line itself.
  - When creating new tables, ensures that the names of the tables are distinct.
  - Allows to customize the appearance of the tables being printed in the terminal.

## Try it Out!

Some sample relations have already been populated in the [`data`](./data/) directory, which are then used by the [`main.cpp`](./main.cpp) to solve some queries! Do give it a look!
