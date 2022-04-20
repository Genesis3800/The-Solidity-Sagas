## State, Local and Global Variables in Solidity.

There are basically 3 types of variables in solidity- Local, State and Global. Let us go through each one of them in detail.


1: **Local variables**

Local variables are the most limited in scope out of the 3 types of variables. Local variables are those which are *declared inside a specific function*. These variables can be called only from the inside of the function, and they *exist only as long as the function is being executed*.
What this means in simple terms is that when a contract is deployed, local variables are not stored on memory in a blockchain, but are only created when the specific function is being called. This saves a lot of gas. For examples, refer to the code snippet below.


2: **State variables**

To put it quite simply, state variables are declared inside a contract, but outside any specific function. This means that any function of the smart contract could use and change the value of those variables.
State variables are needed when a single variable needs to be used more than once to dictate the flow of logic in a smart contract.
When a contract is deployed, state variables are permanently stored on the blockchain. 

Here is a code snippet that shows all the variable types in action.

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract stateVariable {
    
    uint public a =100;
    uint public b = 200;
    uint public c;

    function localExample(uint _x , address _addr) public returns (uint, address, address) { 
        
        uint local1 = 500 + a + _x;
        address localAddr1 = _addr;
        address localAddr2;
        
        c = local1;
        localAddr2 = msg.sender;             // address of the caller, which is a global variable

    return(local1 , localAddr1 , localAddr2);
    }
}
```

See what we do with the variable 'uint local1' . We calculate the final value of the variable based on the parameter passed and an already existing state variable. However, local1 won't exist after the function has been executed fully. To see what value it had, we copied it into the state variable 'c'.


This is a full-fledged smart contract. Don't worry if you can't understand a few lines. We will go over a complete smart contract soon. 

> Note- We tend to use local variables instead of state variables whenever possible. This is because state variables are stored on the blockchain, and hence are more costly compared to local variables. 


3: **Global Variables**

Global variables are the easiest to understand. You don't declare these variables, they are provided to us by solidity and exist in the global workspace. We can use global variables to get the state of blockchain or maybe the address of the one calling the function. They are very useful, and you can go through a list of them [here](https://docs.soliditylang.org/en/v0.8.10/units-and-global-variables.html#block-and-transaction-properties).
We will certainly be using them in the future, and you can take a hint on how they are used from the above code snippet.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650480284880/WUDxqddgF.png)



Now I think we are more than ready to go through a decent smart contract of our own. Stick around for the next blog. Till then, 
GoodBye!!!

