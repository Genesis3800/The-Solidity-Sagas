## Sample Smart Contract- More than Just a "Hello World"

We are now half a dozen posts into our blog. It is high time we wrote a proper smart contract. 
For this post, let us make a simple smart contract that takes in the details of a student, and then returns the details collectively when we ask for them. Simple, right?
This simple smart contract will cover most of the concepts I have covered till now, giving you more clarity. So let's begin.

Any smart contract begins with the following two lines-

```
// SPDX-License-Identifier: MIT
pragma solidity 0.8.10;
```

Line number 1 doesn't have much of anything to do with the smart contract. SPDX is basically a standard for ensuring legal stuff like license compliance, but a smart contract always starts with the declaration of one of these licenses. You can use any one of the licenses listed [here](https://spdx.dev/ids/#how), although I generally go by MIT. You can read more about SPDX over [here](https://en.wikipedia.org/wiki/Software_Package_Data_Exchange).
Now finally onto some real stuff.

'*pragma solidity 0.8.10*' means that our code is suitable for being compiled with **only** the 0.8.10 compiler. It will not compile with any other version.

If I however do this-
' *pragma solidity ^0.8.10* ', then the code with compile with compiler version 0.8.10 or above, but not including any versions of the compiler which are 0.9.0 and above. That is what the ' **^** ' sign implies. Another way of defining the version would be -
'*pragma solidity >=0.4.0 <0.7.0;*'
In this way, the code will compile with any version equal to or above 0.4.0, up until 0.7.0, but not with 0.7.0 itself. 

Defining the version carefully is important because some functions that you are using in your smart contract may not be available with the older versions, or maybe there are some other breaking changes. So choose a version or version range carefully.

Moving on, we do this -

```
contract Function {
        
    struct studentData {

        uint studentID;
        string name;
        string gender;
        uint8 age;
        string class;
    }
    
    studentData[] public studentArray;
```

we start a proper contract by using the keyword 'contract', and any of the private members or functions of the contract are accessible from inside the contract, as we have previously discussed.

> Note- A single solidity file can have multiple smart contracts, and the smart contracts can even inherit each other.
> Yes, solidity supports inheritance.

If you remember from the reference types post, 'struct' is a reference type. Since we need to enter multiple students' data, it is very convenient to store the relevant details of a single student in a single struct. I added some dummy details that we will store for a student using different data types, that we have previously covered.

The last line is interesting.
*studentData[] public studentArray;*
In this line, we are basically **declaring an array of structs.**
A single struct will be stored as a single element in the array, and this is how you would declare such an array.
So this array is what will actually store all of our data together.

> Note- Please go through the syntax carefully from the above code snippets, also in the complete code file which is pasted below.

Now we make the actual function to add the data of a single student to the array-

```
function addToRecord(uint  _studentID, 
                                       string memory _name, 
                                       string memory _gender, 
                                       uint8  _age,  
                                       string memory _class) public  {

studentArray.push(studentData( _studentID, _name, _gender, _age, _class));           
 }

}
```

This function receives all the details of a student as its parameters, and simply pushes them into the array as a struct of type 'studentData'. Nothing more happens here conceptually.
We are **not** returning anything.
However, since we are making changes to a state variable, the function can't be pure or view.
The last curly bracket is the closing bracket of the contract. 

This is it.
Really, this is it.
We do **not** need to make a function to 'view' our array, because the solidity compiler automatically creates a 'getter function' for us to view our variables. Do note that '*studentArray*' is public. If it was private, there would **not** have been such a getter function.

Here is what are sample smart contract looks like right now.


```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.10;

contract Function {

            
    struct studentData {

        uint studentID;
        string name;
        string gender;
        uint8 age;
        string class;
    }
    
    studentData[] public studentArray;

    function addToRecord(uint  _studentID,  string memory _name, string memory _gender, uint8  _age, string memory _class) public {


        studentArray.push(studentData( _studentID, _name, _gender, _age, _class));           
    }   

}
```

> Question- What do you think we would have to do to see our student data if I put a gun to your head and forced you to make studentArray private?
> It should still be possible to see our student Data, right?


To go over the smart contract thoroughly and to give you a nice idea of the entire thing, I made a small video. Please check out the video if you can. I will touch upon some nuances, and you can get a look at the remix IDE first hand too.

%[https://youtu.be/9i4WazhreGE]
