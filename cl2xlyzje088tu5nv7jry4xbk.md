## What is a Constructor in a Solidity Smart contract

If I am appearing for a solidity interview, and the interviewer asks me what a constructor is in solidity, here is what I would say-

"*A constructor is a special kind of function in a solidity smart contract. The core differences are that a constructor is always initialized at the very moment the smart contract is deployed, and that you can only have one constructor for one smart contract.*"

If that seemed too complicated, please bear with me here.
Keep a few things in mind-

- A constructor works almost like any other function of the smart contract. However, the constructor is especially defined by solidity in such a way that it is always called the moment a smart contract is deployed, which makes it quite useful.
- Also you can't declare more than one constructor for a smart contract.

Let us see an example.

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract Constructor {
    address owner;

    constructor( ) {
        owner = msg.sender;
    }
   function displayOwner() public view returns(address){

        return owner;
    }

}
```
> Note- '*msg.sender*' is a global variable. The value of msg.sender is simply the public address of the person who is calling the function at that moment. It is provided to us by solidity.

This simple smart contract shows a basic use-case of a constructor. We declare a variable of the type address.
Then in the constructor, we assign the value of msg.sender to the variable. Do note that it is our own address that will be msg.sender when we are deploying the contract because the constructor is called at the moment of deployment. Hence, the value of the owner is assigned to us.
Now whenever the function displayOwner is called, it will display our address.
How cool!

However, you can also pass all sorts of parameters to a constructor. Here is an example to consider.

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract Constructor {

    string name;
    address owner;
    string initmsg;

    constructor(string memory _name, address _owner, string memory _initmsg){
        name = _name;
        owner = _owner;
        initmsg =_initmsg;
    }

    function displayData() public view returns(string memory, address , string memory){
        return
        (name, owner, initmsg);

    }
    
}
```

Honestly, the code speaks for itself. We initialize a few variables but don't assign them any values. We allow the deployer of the contract to assign values to those variables at the time of deployment.

> Note- When a constructor is defined with parameters, we **have** to provide those parameters at the time of deployment. That is non-negotiable.

That's it. You have learned the basics of constructors in solidity, and you can get started with implementing them in your own smart contract. 
Do drop a like if you found this helpful. 



