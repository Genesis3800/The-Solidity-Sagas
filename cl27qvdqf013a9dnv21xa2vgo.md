## Functions in Solidity

*'Functions'* in programming are basically semi-independent blocks of code. They need to be defined only once and can be called any number of times in the program, thus saving considerable time and effort, while also making the code more readable.

Here is how we can declare a typical function in solidity-

```
function add (uint _x , uint _y) public pure returns (uint) {
uint _sum = _x + _y;
return _sum;
}
```

If you have learned any other programming language, a lot of it would be making sense to you. Nevertheless, let us go through the code snippet.
'*add*' is a function that takes two uint value types as its inputs, and returns another uint *'_sum'* as its result, which is nothing but the sum of those numbers.
Any function that returns something must have the keyword *'returns'* in it's declaration, along with the return type. 
'*return*' and '*returns*' are two totally different keywords, as you can see. 

Now to address the two elephants in the metaphorical room. 
What do the words public and pure stand for? 
'*Public*' is a type of visibility specifier for functions and variables in solidity. Let us go through all the visibility specifiers.

1: **Private**

Private is the strictest visibility specifier in solidity. When a function or variable is declared private, it can only be accessed from within the same contract. This means if the parent contract is inherited by another contract (yes, solidity supports inheritance), even then the specific function can't be accessed.

2: **Internal**

When functions or state variables (I'll get into state variables in a while) are declared as '*Internal*', then they can be accessed *only by the parent contract or the contracts that directly inherit from the parent contract*, not by any other contract. 

Look at the following code snippets-

```
contract parentContract {
  uint internal tempVar;

  function copyFunc() public view returns (uint) {
    uint tempVarCopy = tempVar;

    return tempVarCopy; 
  }

  //ignore externalFunc( ) for now

  function externalFunc() external view returns (uint) {
    uint externalVarCopy = tempVar*2;

    return externalVarCopy; 
  }


}
```

The above snippet shows the declaration of an internal variable, while a public function** from the same contract** is accessing the variable and copying its value, which is okay.

Now look at this- 


```
contract inheritedContract is parentContract {
  function copyFunc2 () public view returns (uint) {
    uint tempVarCopy2 = tempVar;
     return tempVarCopy2; 
  }
}


contract randomContract {
  function copyFunc3 () public view returns (uint) {

        tempContract x = new parentContract();
        x.tempVar;
// Not possible to access tempVar through variable 'X'

  }
}
```

In the above code snippet, all functions of the contract '*inheritedContract*' will be able to access tempVar, while that will not be possible with randomContract. I will ask you to refer to the code snippet while explaining the last two visibility specifiers.


> Quick Question - What do you think would have happened, if tempVar was private instead of internal? Would inheritedContract still have been able to access it? 
Drop down to the comments and answer.

3: **External**
 
When specified as external, the functions can only be called by other functions from outside the parent contract. Other functions from within the same contract cannot call it.

> Note- Only functions can be declared external, not variables.

This means that since externalFunc() was declared as external (refer to code snippet above), both inheritedContract and randomContract could access it, while functions from within parentContract would not be able to access it.
External functions may not make logical sense in the beginning, but they enable us to save gas costs in ways I won't go over right now.

> Note- I don't want to throw you for a loop, but external functions can actually be called from within the same contract too. But for that we have to use '***this***' keyword. I would suggest you to ignore the note for now, if you find it confusing. 
> But do know that if we were to call externalFunc() from within the same contract, we could do so by calling it as '***this.externalFunc()***'

4: **Public**

When functions or variables are declared public, it means that any function of any contract could access the said variables, provided they use the correct syntax of course.



This was all for functions as of now. I know I skipped over what 'pure' stands for, but I will go through that in detail in a post soon. For now, know that there are two types of functions, 'view' and 'pure'. We will discuss them in detail soon. 

