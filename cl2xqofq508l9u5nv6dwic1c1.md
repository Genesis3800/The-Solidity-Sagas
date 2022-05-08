## If-Else and Ternary Operator in Solidity smart contracts

if-Else is part of the syntax of almost all programming languages. It is a basic control structure, but quite useful. Solidity supports many different kinds of control structures, however, we will just take a look at if-else for this one.

Take a look at the code below.

 ```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

contract if_elseif {

    function elseif(uint _x) public pure returns (string memory) {

        string memory val1;

        if (_x < 100) {
            val1 = "number is less than 100";             
        }        
        else if (_x > 100) {
            val1 = "number is greater than 100";    
        }         
        else {
            val1 = "number is equal to 100";    
        }

        return val1;
    }

    function simple_ifelse(uint _x) public pure returns(string memory){

           string memory val2;

        if(_x<100){
            val2 = "x is less than 100";
        }
        else {
            val2 = "x is greater than or equal to 100 ";
        }

        return val2;
    }

    function ternary(uint _x) public pure returns (string memory) {      
        return (_x <= 100 ? "lesser or equal" : "greater" );
    }
}
```
 
This small code snippet is enough to understand both if-else and the ternary operator in Solidity. Let us walk through it.

The first two functions are quite simple. The syntax for if-else and else-if is similar to how it is in other languages. 
The 'Else' conditional is basically a fallback. It is executed if no other condition works out. Function 'elseif' is a good example of that. We check if the given number is greater than or less than 100. If none of those conditions are true, it is only natural that the number be equal to 100.

function 'simple_ifelse' and function ternary serve the same purpose. If we need to use a conditional with only one 'if' condition with a subsequent 'else', we can use either of the two functions.
The ternary operator is basically a compact way of writing the 'if-else'. 
We basically pass a condition to the ternary operator, the syntax of which has been shown above.
If the condition passes, the first return statement is executed, otherwise, the second return statement separated by a colon(:) is executed.

If-else is a simple concept and is used to control the flow of the program. I highly encourage you to paste the code in remix IDE and play around to get a good grasp of it.


