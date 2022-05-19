## Mappings in Solidity- A deep dive

Mappings are one of the reference data types in solidity. For folks who have studied some other programming language, mappings are similar to maps, dictionaries, and hash tables. 

Mappings are basically key-value pairs, and they are often used in place of arrays because it is much faster to search for data inside mappings, as compared to arrays.


1: **Basics of mapping**


This is how mappings are declared.


```
mapping(KeyType => ValueType) variableName

//The mapping below is meant to store the balance of each user(uint) in correspondence with their account address

 mapping(address => uint) public balances;
```

If you need a refresher on the data types in solidity, read [this](https://13thcodearmy.hashnode.dev/value-data-types-in-solidity) and [this](https://13thcodearmy.hashnode.dev/reference-data-types-in-solidity).


Now let us look at a simple mapping example, where we will add and view data in our mapping.

```
contract mappings1 {
    
      mapping(address => uint) public balances;

    function setBalance(address _addr, uint _i) public {

        balances[_addr]=_i;
    }

    function setAutoBalance() public {
        
        balances[msg.sender]=100;
    }

    function getBalance(address _addr) public view returns (uint) {

    return balances[_addr];
    } 

}
```

Let us quickly go over this. In this example, we declare a mapping named 'balances' which will store the account balance of our users, in reference to their account addresses.
In the function *'setBalance'*, we use two parameters, of the types address and uint respectively. In the function, I show you how you could add data to your mapping. We update the balance of the given address with the given amount of balance.

In the second function '*setAutoBalance'*, I use the global variable *'msg.sender'* to set the balance of whoever called the function as 100.

The function *'getBalance'* is simply a function that returns an element of 'balances'(The name of our mapping variable).
Keep in mind that the type of return value is 'uint', not 'mapping'. In the function, we return the balance of the *'_addr'* address and remember that the balance is stored in 'uint' type. 


> Note- The following mapping declaration is invalid:
    
> mapping( struct => address) public balances2;

> This is because the keyType cannot be any reference type. It can be any built-in 
> value type, bytes, string, or any contract, but not a reference type. I highly 
>  recommend you to go through a link above to read more about solidity types.


2:  **Mapping detailed Example**


Let us say someone is donating you some crypto coins. 
You may want to store their details, right? 
How about we create a mapping that stores the details of our benefactors against their addresses. That would be pretty cool.

Have a look at this-

```
contract detailedMappings {

  struct Donor{
      string name;
      uint age;
      string addr;
      uint donation;
  }

  mapping(address => Donor) donor_info;

  function setDetails(string memory _name, uint _age, string memory _addr, uint _donation) public {

      Donor memory temp;
      temp = Donor(_name,_age,_addr,_donation);

      donor_info[msg.sender] = temp;
  }

  function getDetails(address _addr) public view returns(Donor memory) {
      return donor_info[_addr];
  }

  function deleteDetails(address _addr) public {
      delete donor_info[_addr];
  }

}
``` 

In this example, we create a struct by the name of 'Donor', which stores all the relevant details of our hypothetical benefactor, along with his address of residence. We then store these details alongside the account address from where we receive the donation in a mapping. 
Hence, our key type is address, and our value type is 'Donor', a struct.

> Note- We cannot have structs as key types. Also know that 'Donor' will now be used as a data type in itself, as will be clear from the code snippet.
> Our value types can be of any type, even of type contract, but there are restrictions on what kind of data can be a key.

In the function  *'setDetails()'*, we ask the user to pass on his details, along with his donation amount. We then store those details in our mapping, against the address through which he sent us the donation.

The function *'getDetails()'* is quite straightforward, but do note something. When we return the value, we return a variable of type 'Donor', as defined in the beginning of the contract. 

The function *'deleteDetails()*', does as the name suggests. The function will delete the value, in mapping, of the address that has been passed as the parameter to the function. We use the delete keyword given to us by solidity.


3: **Nested Mappings**

Nested mapping refers to the practice of creating a mapping with a key type of another mapping.

Let us go through this code snippet.

```
contract nestedMapping {
    
    mapping(address => mapping(string => uint)) public nestedMap;   

    function set(address _addr1, string memory _name, uint _balance) public {
        nestedMap[_addr1][_name] = _balance;
    }

    function get(address _addr1, string memory _name) public view returns (uint) {
        return nestedMap[_addr1][_name];
    }

    function remove(address _addr1, string memory _name) public {
        delete nestedMap[_addr1][_name];
    }
}
```

Here, we create a mapping named nestedMap which in turn takes a mapping as it's valueType.
By now you should be clear with the basics of mapping, and the above code merely adds to the mapping, displays it, and deletes a value from it. If you understood the earlier code, this should be pretty self-explanatory.

> Note- You can't return mapping from a function in solidity.
> It sucks, I know.
> If you see carefully in the function 'get()', we return a type of uint after accessing the child mapping within our parent mapping.

        

