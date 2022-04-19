## Value Data Types in Solidity

Hi there, welcome to the first proper post on the blog. If you haven't done so, I strongly recommend that you go through the [introduction](https://13thcodearmy.hashnode.dev/the-solidity-sagas-what-will-it-be-about) of the blog.

I believe that the basic data structures of a programming language are the best thing to start with while learning the language. So without much further ado, lets us dive right in-

Solidity broadly provides us with two types - Value and Reference.

The difference is simple. A value type stores its own value, nothing else. A reference type on the other hand stores the *Location Of the Data it is Referring to*, hence the name 'reference type'. In practice, this leads to minor differences in how these types are used, which I will cover in later posts.

Value types however are as follows-


1:  **Booleans (bool) -** 

This data type is the simplest of all, and it accepts only two values- 'true' and 'false'.

You would declare bool data types in solidity as follows-

```
    bool public tempBool = true;
    bool public tempBool2 = false;
```

> Note- Variables and functions in solidity are typically declared with a visibility quantifier like 'public' or 'private'. This defines the accessibility of the variable or function, and we will go through them in detail in a later post. We will be looking at just public variables and functions for now.





2:  **Integers (int/uint) -**

If you have worked with other programming languages, you would know that these languages typically have a data type to store integers, usually denoted by *'int'*. 
Solidity however has a dedicated type for storing positive integers, denoted by *'uint'*.

uint stores only positive integers as acceptable values.

Here is how you would declare integers in solidity - 

   ```
    uint8 public tempInteger = 21;
    uint32 public tempInteger2 = 99;
    int public tempInteger3 = -22;
```

Wondering what the 8 stands for in 'uint8'? No worries, I got you covered.
See, integers in solidity are restricted to a certain range. for example, 'unit8' would have a range of  ( 0 to 2(pow(8))-1 ). The range can be increased in steps of 8 up to 256. Thus, the maximum value of an integer in solidity can be *2(pow(256))-1*.

> Note- When the size of an int/uint is not explicitly defined, solidity initialises them with a size of *'256'*. Hence, 'int' is equivalent to 'int256'.
> 
> Quick question. What do you think will be the range of tempInteger3 ? 
> Comment below.



If you think about it, having a dedicated data type to hold only positive integers makes a lot of sense. Solidity is mainly used to write smart contracts, which in themselves are basically a logic-dictated flow of money. If you are sending and receiving money, you can't have the balances going below zero, because that would mean nothing. 
How would you feel if I ***'Gave'***  you ***'-10 Ethers'***  ? Ponder on this for a minute.




3:  **Address ( address / address payable )** -

'address' is a special kind of data type, unique to solidity.
The EVM supports the transfer and receiving of funds between smart contracts deployed on different '*addresses*'. This is where the type address comes in.

In general, a variable of the type 'address' holds 20 bytes, the general size of an Ethereum address. To make an address capable of receiving Ether, you have to declare it as an 'address payable', or else it can't be sent ether.

```
     address public tempAddr1;
     address public tempAddr2 = 0x165CD37b4C644C2921454429E7F9358d18A45e14;
```

> Note- When you don't initialise a variable with a specific value in solidity, it is by default assigned a zero-value. For example, an uninitialised bool type will be assigned a value of 'false', while an equivalent variable of type int will be assigned a value of 0.







This is it for the first post. I realize this post only contains variable declarations for 'code', but that is by design. Next, I will take you through some complex data types and the types of functions and their purposes in a solidity smart contract.
After that, we will go through a few sample smart contracts which will enable you to understand what is going on inside a smart contract much more easily.






    





