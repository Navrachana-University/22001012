# TAC Generator for French-C-Like Language

## Project Description

This project implements a compiler frontend that translates source code written in a simplified C-like programming language with French keywords (e.g., `imprimer` for print, `si` for if, `sinon` for else) into Three-Address Code (TAC). Built using [Bison](https://www.gnu.org/software/bison/) for parsing and [Flex](https://github.com/westes/flex) for lexical analysis, it showcases fundamental compiler design concepts. The generated TAC is output to `output.txt`.

## Author

- **Ronit P Girglani 22001010**
- **Kenil Patel 22001012**

## Included Files

- `parser.y`: Bison grammar file defining the language syntax and TAC generation logic.
- `lexer.l`: Flex lexer file specifying token patterns, including support for French keywords and accented characters.
- `Lab Manual`: Lab manual provided as part of the assignment requirements.
- `tac_generator.exe`: executable file.

## Setup and Running Instructions

### Prerequisites

- **Bison** and **Flex**: For generating parser and lexer.
- **GCC**: For compiling the generated C code.
- A Unix-like environment (Linux, macOS, or WSL on Windows) is recommended, But it is possible to use Windows 11.

### Steps to Build and Run

1. **Clone the Repository**:
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```
2. **Generate Lexer and Parser**:
   ```bash
   flex lexer.l
   bison -d parser.y
   ```
3. **Compile the Code**:
   ```bash
   gcc lex.yy.c parser.tab.c -o tac_generator
   ```
4. **Run the Program**:
   - Create an input file (e.g., `input.txt`) with source code using French keywords.
   - Example input:
     ```
     x = 5;
     si (x == 5) {
         imprimer x;
     }
     ```
   - Execute:
     ```bash
     ./tac_generator input.txt
     ```
   - The generated TAC will be written to `output.txt`.

## Special Instructions

- Use French keywords (e.g., `imprimer`, `si`, `sinon`) in the input file, as defined in `parser.y`.
- The lexer supports accented characters (e.g., é, è, ê) in identifiers, enabling French-specific variable names.
- Ensure your terminal and text editor use UTF-8 encoding to handle accented characters correctly.

## Example Usage

### Input File (`input.txt`)

```
x = 5;
si (x < 0) {
    imprimer "negative";
}sinon si (x == 0){
    imprimer "zero";
}
sinon {
    imprimer "positive";
}
```

### Expected Output

```
ifFalse x < 0 goto L2
print "negative"
goto L3
L2:
ifFalse x == 0 goto L0
print "zero"
goto L1
L0:
print "positive"
L1:
L3:
```

The program generates TAC in `output.txt`, following a standard three-address code format with at most three operands per instruction.

