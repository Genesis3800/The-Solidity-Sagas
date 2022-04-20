## View and Pure Functions in Solidity

This will be a short post, because trust me the concept of view and pure isn't difficult to understand. Let us get on with it.
Only after publishing this article, did I realize you need to know about state and local variables before going through this post. You can read about them [here](https://13thcodearmy.hashnode.dev/state-local-and-global-variables-in-solidity).


1: **View Functions**

View functions are those functions that can read, use and return any state variables that exist in the smart contract. 
The only rule is that they can't make any change to any state variable.
Thus, any function that merely reads a state variable without making any change to it can be a view function.

If you look at the code snippet below, viewFunc1 merely returns tempInteger as it is, whereas viewFunc2 returns a different value. 
They are both however view functions since viewFunc2 does not make any change to the value of tempInteger itself. If it changed the value of tempInteger, it would not remain a view function.

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract viewAndPure {
    
    uint public tempInteger =30;

    function viewFunc1( ) public view returns (uint) { 
     return tempInteger;
    }

    function viewFunc2( ) public view returns (uint) { 
    return tempInteger+50;
    }

    function pureFunc1( ) public pure returns (uint) { 
     return 1;
    }

    function pureFunc2(uint _x , uint _y ) public pure returns (uint , uint) { 
     return _x + _y;
    }
}
```


2: **Pure Functions**

Pure functions are even more restricted than view functions. A pure function is not only forbidden from making any changes to state variables, it is forbidden to even read them. A pure function therefore can't make any calculations that use any state variables as its component. 
As seen in the code snippet above, pureFunc1 returns that value '1' always, while pureFunc2 simply returns the sum of the parameters it receives, hence avoiding any state variable entirely.



That's it. Really. That is all there is to know about view and pure functions. If any function is defined without using either of the two keywords, it can read and manipulate any state variable of its smart contract without restriction. I think that is called a '*simple*' function.
