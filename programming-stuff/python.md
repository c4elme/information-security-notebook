## **Codecademy Course**

```
""" this is a comment block """
```

**Defining a function**

```
def function_name(parameter):
   codes = "here"+parameter
   return codes
print(function_name(argument))
```



Pulling in just a single function from a module is called a function import, and it's done with the from keyword:

```
from module import function
```

```
# Import *everything* from the math module on line 3!
from math import *
```



```
import math # Imports the math module
everything = dir(math) # Sets everything to a list of things from math
print everything # Prints 'em all!
```

Some functions/built-in functions

```
min()
max()
sqrt()
pow()
abs()
type()
.lower()
.upper()
```

Example Codeblocks

```
def function_name(param):
    if type(param) == int or type(param) == float:
        print abs(param)
    elif type(param) == str:
        print "str"
    else:
        print "nope"

function_name()

#example for loop
array = ['asd','dsa','sss','ddd']
for x in array:
    print(x)

#other for loop examples
# Prints out the numbers 0,1,2,3,4
for x in range(5):
    print(x)

# Prints out 3,4,5
for x in range(3, 6):
    print(x)

# Prints out 3,5,7
for x in range(3, 8, 2):
    print(x)
```



