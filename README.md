# TuckyParser
A simple to use argument parser library for C

## Table of Contents
* [Install and Building](#install-and-building)
    * [Git](#git)
* [Examples](#examples)
* [Usage](#usage)
* [License](#license)

# Install and Building
## Git
First, clone the repository to your prefered location and copy the header to your project.
Then, build with your favorite system.
```bash
git clone https://github.com/jhendle2/tuckyParser.git
cd tuckyParser
cp tuckyParser.h /TO/YOUR/PROJECT
```

## Examples
```c
#include "tuckyParser.h"

int main(int argc, char** argv) {
    TuckyArgParser parser = newArgParser(argc, argv);

    addArgument(&parser, 'f', "file"   ,    AS_MANY, REQUIRED, "Input file path");
    addArgument(&parser, 'o', "out"    ,          1, REQUIRED, "Output file path");
    addArgument(&parser, 'v', "verbose", STORE_TRUE, OPTIONAL, "Enable verbose output");

    parseArgs(parser);

    TuckyArg file_args = getArgumentFromFlag(parser, 'f')->args;
    printf("input    = ");
    TUCKY_FOREACH(arg, file_args) {
        printf("%s ", arg->txt);
    } printf("\n");

    printf("output   = %s\n", getArgumentFromFlag(parser, 'o')->args->txt);
    printf("verbose? = %s\n", getArgumentFromFlag(parser, 'v')->enabled ? "TRUE" : "FALSE");

    delArgParser(parser);
    return 0;
}
```

## Usage
```bash
> ./myApp --file test1 test2 -o test3 -v
input    = test1 test2 
output   = test3
verbose? = TRUE

> ./myApp -h
#######################################
# YourAppName v0.0.0
# Author: John A. Smith
# Last Modified: Jan 01, 1989
#######################################
==== ./main ====
  -h --help       [0] : Display the help information
  -f --file       [∞] : Input file path
  -o --out        [1] : Output file path
  -v --verbose    [0] : Enable verbose output
```

## License
Written by: Jonah Hendler (jhendler17@gmail.com)

[GNU GENERAL PUBLIC LICENSE](LICENSE)