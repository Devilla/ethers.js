-----

Documentation: [html](https://docs-beta.ethers.io/)

-----

ContractFactory
===============

Creating Instances
------------------

#### **new ***ethers* . **ContractFactory**( interface , bydecode [ , signer ] )



#### *ContractFactory* . **fromSolidity**( compilerOutput [ , signer ] ) => *[ContractFactory](/api/contract/contract-factory/)*



#### *contractFactory* . **connect**( signer ) => *[Contract](/api/contract/contract/)*



Properties
----------

#### *contractFactory* . **interface** => *[Interface](/api/utils/abi/interface/)*



#### *contractFactory* . **bytecode** => *string< [DataHexString](/api/utils/bytes/#DataHexString) >*



#### *contractFactory* . **signer** => *[Signer](/api/signer/#Signer)*



Methods
-------

#### *contractFactory* . **attach**( address ) => *[Contract](/api/contract/contract/)*

Return an instance of a [Contract](/api/contract/contract/) attched to *address*. This is the same as using the [Contract constructor](/api/contract/contract/#contract--creating) with *address* and this the the *interface* and *signerOrProvider* passed in when creating the ContractFactory.


#### *contractFactory* . **getDeployTransaction**( ...args ) => *[UnsignedTransaction](/api/utils/transactions/#UnsignedTransaction)*

Returns the unsigned transaction which would deploy this Contract with *args* passed to the Contract's constructor.


#### *contractFactory* . **deploy**( ...args ) => *Promise< [Contract](/api/contract/contract/) >*

Uses the signer to deploy the Contract with *args* passed into tgee constructor and retruns a Contract which is attached to the address where this contract **will** be deployed once the transction is mined.

The transction can be found at `contract.deployTransaction`, and no interactions should be made until the transaction is mined.


```
// <hide>
const signer = ethers.LocalSigner();
const ContractFactory = ethers.ContractFactory;
// </hide>

// If your contract constructor requires parameters, the ABI
// must include the constructor
const abi = [
  "constructor(address owner, uint256 initialValue)"
];

const factory = new ContractFactory(abi, bytecode, signer)

const contract = await factory.deploy("ricmoo.eth", 42);

// The address is available immediately, but the contract
// is NOT deployed yet
contract.address
//!

// The transaction that the signer sent to deploy
contract.deployTransaction
//!

// Wait until the transaction is mined
contract.deployTransaction.wait()
//!

// Now the contract is safe to ineract with
contract.value()
//!
```
