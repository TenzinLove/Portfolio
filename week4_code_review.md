# Code review

This section documents your practical work from week 4 in which you attempt a series of 
code review challenges. For your portfolio, do the following:

1. Choose the code review challenge which best demonstrates your skills.
2. Copy the code into your portfolio using a Markdown
   [fenced code block](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks).
3. Provide some descriptive commentary that identifies the problems.
4. Show your improved version of the code in a second code block.
5. Explain in one or more paragraphs why your solution is a good one.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -



Here is the code I chose to work on:

```

using System;

namespace MyApplication
{
  class Program
  {
    static bool check(Int i) 
    {
        if (i % 2 == 0)
        {
            return true;
        }
        return false;
    }

    static void Main(string[] args)
    {
        //... Code not shown - ignore this line
    }  
  }
}

```

It's a code about which there are some interesting things to say.


Firstly, the code doesn't respect the standard C# coding conventions. Indeed, we assign an "Int" 
to the variable i instead of assigning it an "int" with a lowercase i.

Moreover, the method "check" isn't explicit enough because we don't know what we're checking; 
just like the variable "i", which doesn't correspond to anything. We can replace "check" with "IsEven" and "i" 
with "TheNumber" or "NumberToCheck", for example. These changes make the code easier to read.

To finish, we can simplify the "check" method by removing the "if" loop and returning the result directly.

Here is the code modified: 

```

using System;

namespace MyApplication
{
  class Program
  {
    static bool IsEven (int NumberToCheck) 
    {
        return NumberToCheck % 2 == 0 ;
    }

    static void Main(string[] args)
    {
        //... Code not shown - ignore this line
    }  
  }
}

```

In conclusion, the improved code simplifies the method "check" by giving it a more descriptive name, 
"IsEven," which immediately makes its purpose immediately obvious: determining if a number is even or odd. 
By removing the "if" statement and directly returning the result of the condition directly, the code 
becomes more concise.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
