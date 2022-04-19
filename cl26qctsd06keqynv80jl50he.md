## Reference Data Types in Solidity

'Reference' types are complex data types that don't usually fit into 256 bits(32 bytes). An important point to know is that the reference types *don't store the actual value*. They merely store a reference to it. This means that if two reference types point to a single piece of data, then a change in one of those reference types will cause a change to the other. This is why reference types have to be used carefully. 

Currently, reference types comprise of arrays, structs, and mappings.

1:  **Arrays( valueType arrayName [ sizeOfArray] )** -
 
Arrays are common in most programming languages. An array is basically a data structure that stores multiple values of a *single value type* in sequential order. This makes it easy to access multiple values from a single variable.
This is how we would declare a fixed-size array-

```
    uint tempArr1 [10];                            
    uint tempArr2 [5] = [1, 2, 3];
    uint tempArr3 [] = [1, 2, 3, 4, 5];
    uint[] tempArr4;                                      
```
When we declare an array like we declared tempArr3, the size of the array becomes equal to the number of values we initialised it with. Whereas, tempArr4 is a dynamic array with an undetermined size.

Here are the two main Array methods offered to us in solidity- 

- Length: *Arr.length* will return the size of an array. We can check the size of a fixed-size array, or assign a new size to a dynamic array using this method.

- Push/Pop: *Arr.push* and *Arr.pop* don't return anything. Push merely inserts a new element towards the end of the array, while Pop removes the last element of the array.


> Note- Arrays in themselves are a huge topic. They can be fixed size or dynamic, they can store simple value types or complex types like struct and mappings. You can also store multiple reference types in a single array. All of this will be explored in detail in later posts.


2: **Structs (struct)** -

Structs are basically a collection of different value types, sort of like a record. Say you want to store the details of a student. You would need data points like student ID, Name, age, marks, residential address, etc. All of these would be of different value types, but we could group them nicely into a struct.

```
struct tempStruct  {

    uint studentID;
    string Name;
    uint age;
    uint marksPercentage;
    string residence;
}
```
This is what a basic struct would look like. This is now a custom data type that you just created. Congratulations!

We can now initialize variables with the struct as a data type.

```
    tempStruct[] private studDetails;
```

We now have an array of the value type of tempStruct, with the name studDetails which we have kept private. We can push data into the array by using array methods inside functions. We will see all of this and more soon enough when we make a new smart contract from scratch.


3: **Mappings (mapping(keyType => valueType))** -

Mappings are basically key-value pairs. They hold two values in tandem to be called when needed. 
The 'key' can be of any primitive value type, along with bytes or strings. The value type on the other hand can be of any type.
Mappings can be of any length.

Here is what the basic syntax of declaring a mapping type along with adding values to it will look like.

```
mapping(address => uint) public balances;

     function update(uint newBalance) public {
         balances[msg.sender] = newBalance;
      }
```

This small code snippet initializes a mapping and adds a pair of values to it using the function '*balances*'. msg.sender is basically the address of the person accessing the function. Hence, whatever be the value of newBalance, that specific address will get that much of the token.

Now hear me out, these reference types in solidity are a doozy and a half, so I have left quite a bit while starting out with the basics. I have no qualms in admitting that even after a month of learning in the field, I struggle with the advanced concepts of these value types. In the next post, we will see how functions work in solidity, following which we will try to write our own smart contract.





 