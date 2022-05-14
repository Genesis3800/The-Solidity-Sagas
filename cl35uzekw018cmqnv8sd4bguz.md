## Create your own ERC20 Token in under 5 min on Polygon

Prerequisites for following this tutorial-

1. Basic knowledge of how a smart contract is structured, along with the very basics of solidity. You can learn basic solidity quickly from my blog posts [here](https://13thcodearmy.hashnode.dev/series/thesoliditysagas). 

2. You need some Test Matic on the Mumbai testnet. If you don't have test Matic, you can get them over [here](https://mumbaifaucet.com/).

With that covered, let's dive in.

So what exactly is OpenZeppelin?

See the thing with smart contract development is that they need to be **absolutely** secure. They can't have any bugs or vulnerabilities in them, because smart contracts directly handle money, sometimes large amounts of them.
This makes it imperative to make them as secure as possible.
So instead of reinventing the metaphorical wheel every time we write a basic smart contract, we opt to use previously written smart contracts which have been thoroughly audited by the experts in the community. 
OpenZeppelin is one of the best libraries in the space to offer such a service.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652529372721/UFFpqpwB0.png align="left")

Here I am at the OpenZeppelin [Contracts Wizard](https://docs.openzeppelin.com/contracts/4.x/wizard).

This wizard allows you to quickly put together your own smart contracts built on the pre-existing OpenZeppelin contracts. You can pick and choose your desired features.

In our ERC20 contract, we have chosen just one feature, the mintable feature. What this function does is that it allows us, **only us** to mint more of our tokens to the people we desire. That's it. This gives us a basic ERC20 smart contract. 

Now let us quickly go through some important code, before we deploy the contract.

```
constructor() ERC20("OpenZ Demo", "OZD")
  {
        _mint(msg.sender, 1000 * 10 ** decimals());
  }
```
 

This is how a basic constructor is written in solidity. A constructor is a special kind of function **which runs only once** when the contract is deployed. A constructor can **not ** be called after that. We use it to set some initial values as per our requirements.

In this specific constructor, we pass it 2 arguments, the token name, and the Token symbol as is shown in the snippet above.
Then we call the function '_mint', which is defined in the [ERC20 smart contract](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.6.0/contracts/token/ERC20/ERC20.sol), which we are inheriting.

'msg.sender' is nothing but the address of the person who is calling the function. Since we call the constructor at the time of deployment, we are the ones calling it.
'decimals()' function returns nothing but the number 18. Thus, the second parameter to the mint function is (1000^18). 
Why the power 18?
Well, that is because an individual token can be broken down into 18 decimal places. Thus we mint the token in terms of its smallest unit. 

> Note- How many tokens do you think would be minted, if we changed the parameter to (1000^19)?

Now let us move to the function 'mint', which is different from the function '_mint'.
Confusing, I know. But the name differences are important to keep in mind. 
The 'mint' function is very simple. It mints the desired quantity of our token to the recipient's address. The 'only owner' that you see written next to the function declaration is called a modifier. Modifiers allow us to control access to a function, and in this case, the modifier allows only the deployer of the contract( which is us) to mint the tokens. 
Cool, right?

That's it, we are done with our smart contract. Now let us deploy it.
For that open the [Remix IDE](https://remix.ethereum.org/) and create a .sol file under the contracts folder, and simply paste the code from the OpenZeppelin wizard.

After pasting the code into the editor, go to the compile tab on the left and compile the contract. It may take a while the first time around.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652531427023/wimGqeH-b.png align="left")

Then switch on to the deploy tab, just below the compile tab.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652531404377/5J2Pif5UX.png align="left")

Now do two simple things.

1. Switch the environment from the default to 'Injected Web3'.

2. Go to the contracts drop-down, and choose carefully the contract that **you** created.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652531779511/Td5NBBT5J.png align="left")

Now when you click on deploy, Metamask should pop up.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1652531890599/N1YBKTKmi.png align="left")

> Note- Before you click on deploy, make sure you are on the Mumbai testnet, or on any other EVM compatible chain. You could even deploy to a mainnet if you want.

Now click on confirm inside metamask, and then after a few moments you can see the successful deployment on mumbai.polygonscan.com . 

That's it.
You now have your very own token on the polygon testnet, and it is ready to be deployed on the polygon mainnet.
Congratulations on completing the tutorial.
Stay tuned for more such OpenZeppelin tutorials.













