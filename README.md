# Extending P0 compilers with typed Maps

## Authors:
- **Usman Asad**
- **Muhammad Faisal Jaffer**
- **Aleem Haq**

# High level explanation of our typed map implementation

**Authors: Aleem Haq, Usman Asad, Muhammad Faisal Jaffer**

**Computer Science 4TB3**, ***McMaster University***

## Cuckoo Hashing

- Uses 2 hash functions (Hash1, Hash2)
- Uses 2 arrays to store references to the key-value pair (Array1, Array2)
- Hash1 determines the index at which to place the key-value pair in Array1. Hash2 determines the index at which to place the key-value pair in Array2
- Inserting a key-value pair, Array1 is first used to insert. If Array1 has an element stored at that index, then the existing element is placed in Array2 and the new element is placed in the Array1. If Array2 has an element stored at the index, Array1 is used to store the existing element. 
- If a loop is detected, the array sizes are increased by 2x and hash functions are rehashed.


## Our map in memory
`[ size | array1 ref | array2 ref | numOfRecords]`

## Our array in memory
`[ size | node1 ref ... nodeN ref]`

## Our node in memory
`[ key | value ref]`

# File Structure

The main directory includes the following files/folders:

- [**map.ipynb**](./map.ipynb) - Web Assembly function by function Maps implementation and documentation

- [**design_decisions**](./design_decisions.md) - A document highlighting the design decisions for the project

- [**Readme**](./README.md) - This readme file for navigating the project

- [**project_proposal**](./project_proposal.md) - A document that outlines the project, plan and resources

- [**Map**](./Map/) - A folder with a collection of notebooks for the entire implementation of extending P0 compiler with Maps

- [**Presentation**](./Presentation/) - Includes project presentation slides in pdt and pptx format



The actual implementation and extension of the P0 compiler with typed Maps is implemented across the following notebooks in the [**./Map**](./Map/) directory:


- [**ST.ipynb**](Map/ST.ipynb) - P0 Symbol Table (added support for Maps)

- [**SC.ipynb**](Map/SC.ipynb) - P0 Scanner (added support for Maps)

- [**P0.ipynb**](Map/P0.ipynb) - The P0 Compiler (added support for Maps)

- [**CGwat.ipynb**](Map/CGwat.ipynb) - P0 Code Generator for WASM (added support for Maps)

- [**Map Prototype.ipynb**](Map/Map_Proto.ipynb) - Map implementation in web assembly

- [**Sample Syntax.ipynb**](Map/Sample%20Syntax.ipynb) - Map syntax and examples

- [**Run Time Tests.ipynb**](Map/RunTimeTests.ipynb) - A collection of run time tests for look up and insertion time

- [**Error Testing.ipynb**](Map/error_testing.ipynb) - A collection of P0 programs to test expected errors/exceptions

  

## P0 Symbol Table

  

Added Map type for Symbol table entries.

The P0 Map is represented by an object of class Map. For Map's the keyType and valueType are kept as the fields of the class. The other field is lvl which is used to track whether or not the Map has been initialized.

  

```

class Map:

def __init__(self, keyType, valueType):

self.keyType, self.valueType, self.lvl = keyType, valueType, 0

def __str__(self):

return 'Map(key type = ' + str(self.keyType) + ', value type = ' + \

str(self.valueType) + ', level = ' + str(self.lvl) + ')'

```

  

## P0 Scanner

  

Added Map associated symbols and keywords to the scanner.

Note: Symbols are encoded by integer constants.

  

```

Map = 52;

INIT = 53; INSERT = 54; GET = 55; LEN = 56; IN = 57;

```

  

Adding to the keywords for the `identKW()` procedure:

  

```

KEYWORDS = \

{...'Map': Map, 'init': INIT, 'insert': INSERT, 'get': GET, 'len': LEN, 'in': IN}

```

  

## P0 Compiler

  

- Import Maps and supporting logic from Scanner and Symbol table:

```

from SC import Map, INIT, INSERT, GET, LEN, IN

from ST import Map

```

  

- Extend P0 grammar(Selector, Expression, Statement and Type) and parser with Map properties

  

- Type for Maps:

  

```

Map <key_type, value_type>

```

  

- Selector for Maps:

```

.get(n)

```

- Expression for Maps:

```

"in"

```

- Statement for Maps:

```

...ident ".init" |

ident ".insert(" expression, expression ")"

```

  
  

## CGwat

Added the following code generation procedures:

- `genInitMap(x)` is used to intialize a Map in memory so that it operations can be done on it.

- `genInsertMap(x,key,value)` is used to generate the code to insert a <key,value> pair into the Map, it is able to deal with using vars or constant's as the key's and values.

- `genGetMap(x,key)` generates the code to get the value at key `key`.

- `genMapLen(x)` generates the code accessing the number of records that have been inserted into the Map, ie the length of the Map.

- `genInRelation(x,y)` is used to generate the code checking if key x is in Map y, it supports the cases where x is a const value or if it is a variable

## Map Prototype

Contains the implementation of Maps using Cuckoo hashing in web assembly. Note that this notebook is used by the P0-CGwat for extending the P0 compiler with Maps.

  

We have a formal documented version of this notebook **Map.ipynb** which is present in the parent folder. Please refer to that notebook and the documentation within, to get an understanding of the Maps in Web assembly.

  
  

## Syntax

The following sections show the syntax for using Maps in P0.

### Map declaration

`var example: Map <type₁, type₂>` where type₁ & type₂ can be any 32 bit word, and example can be any variable name that fits within the P0 compiler.

  
  
  

#### The Map `example` defined above will be used as an example for the following definitions

### Use of Functions

The way to use the Map's functions is to add a `.` after the variable name, followed by a command. e.g. `example.init`

  
  

### Initialization

`example.init` initializes the Map. This needs to be done once after declaration in order for you to use the Map that you defined

  

### Insertion

`example.insert(key,value)` is used to insert a value into the Map. The key and value have to be of types; `type₁`, and `type₂` respectively. If not an exception is thrown.

  

### Get

`example.get(key)` is used to get the value of the key given. If the key does not exist an error is thrown

### Length

`example.len()` is used to return the number of entries in the Map.

  

Sample P0 program with Map:

  

```Pascal

program sampleMap

var x, y: integer

var m: Map <integer, integer>

m.init

x ← read(); y ← read()

m.insert(x,y)

write(m.len())

write(m.get(x))

m.insert(2, 12)

if 2 in m then write(0)

```

  

## Run Time Tests

Includes run time tests to examine performance of the Maps implementation.

  

Contains P0 programs that insert **key,value** pairs into a Map.

Each program has different number of Map's insert commands (executed in a while loop), followed by Map's look-up command, which are timed and compared to make sure the insertion and look up times are constant, irrespective of the size of the Map.

  

## Error Testing

Includes tests for the following errors related to Maps implementation:

  

- Exception: **Map not initialized**

- Exception: **Map key type mismatch**

- Exception: **Key does not exist**

- Exception: **Key expected to be Int, Bool, Set**

  

And tests for several syntax errors:

- Exception: **Dedent or new line expected**

- Exception: **')' expected** etc..