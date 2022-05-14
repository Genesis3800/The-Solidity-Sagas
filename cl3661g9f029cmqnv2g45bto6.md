## Arrays in Solidity- A deep dive.

Arrays in solidity are of two types-
Fixed and Dynamic.

If you have worked with any other programming language, you would have probably figured out the difference.
Fixed arrays have their size declared at the time of declaration, while dynamic arrays can have varying sizes as the code runs.

I made a cool little code snippet to go along with the tutorial. Don't be afraid of the code, we will walk through all the functions together.

The first thing to note is the difference in the declaration of fixed and dynamic arrays.
The two fixed-size arrays are initialised with their sizes declared, but the same is not true for dynamic arrays.

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;

contract Array {

    // Fixed sized array
    uint[15] public arr1 = [9,8,7,6,5,4];                  
    uint[3] public arr2 = [1, 2, 3];

    //Dynamic Array
    uint[] public arr3 = [1,2,3,4];

    //Looking at the lengths of the Arrays
    function _Len1 () public view returns(uint){
     uint len1 = arr1.length;
     return len1;
    }

    function _Len2 () public view returns(uint){
     uint len2 = arr2.length;
     return len2;
    }

    function _Len3 () public view returns(uint){
     uint len3 = arr3.length;
     return len3;
    }

    //How to return an array
    function returnArr1() public view returns (uint[15] memory) {
        return arr1;
    }

    function returnArr3() public view returns (uint[] memory) {
        return arr3;
    }


    //Traversing an Array
    function _Array1OP() public {
        for(uint i=0; i<arr1.length; i++)
        arr1[i]*=10;
    }

    //declaring a fixed array in memory
    function _memArr() public pure returns(uint[] memory){
        
        uint[] memory memArr = new uint[](5);

        for(uint i=0; i<3; i++)
        memArr[i]=i;       

        return memArr;
    }

    //How to Delete an element.
    //Deleting an element MERELY CHANGES IT TO 0, does not actually remove the index
    function _deleteElement() public{
        delete arr1[1];
        delete arr2[1];
        delete arr3[1];
    }

    //Push and Pop in a dynamic array
    function _pushPop() public {
        arr3.push(1000);
        arr3.push(2000); 
        arr3.pop();
    }

}
```

Now look at the three similar functions, '_Len1()','_Len2()', and '_Len3()'.
They simply return a variable that tells us their respective lengths.
'.length' is the function that simply gives us the length of the array. The lengths of both types of arrays are returned in the same way.

> Note- The length of arr1 is **NOT** 6, the number of elements it contains. What do you think it's length is?

Functions returnArr1() and returnArr3() return to us the entire arrays. We have to pass a parameter of type 'Array' to the 'returns' bracket, and there is a very minute difference between the two parameters.

Function _Array1OP() shows how to run a basic operation on an array. It will be the same way for dynamic arrays too. We simply run a for loop to multiply each element by 10.

Function _memArr() is important. It shows you the syntax to declare new arrays locally, inside a function itself. Then we run a small for loop to fill it with 3 values.

> Note- You **cannot** declare dynamic arrays inside a function. That is not allowed. Also, for reasons beyond the scope of the article, it is generally advised to not declare arrays inside a function.

Function _deleteElement() uses the delete keyword to 'delete' the value of the 2nd element of each array. Please note that the array element is **NOT** removed, only the value of the specific element is changed to zero. We will look at how to properly remove an element from an array in the next post.

Now the final function, _pushPop(). Push function merely 'pushes' AKA inserts a specific value in an array at the end of the array.
While the Pop function removes the last element of the array. It is that simple.

I have prepared the small code snippet for you. I **strongly** recommend you to copy it into the online remix IDE and try to play around with the functions and see how the values change. It will give you clarity in your concepts.
If you liked the article, please consider dropping a like. 

Stay tuned for more :)



