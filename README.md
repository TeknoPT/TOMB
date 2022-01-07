# TOMB
TOMB smart contract compiler for Phantasma platform

<p align="center">      
  <a href="https://github.com/Relfos/TOMB/workflows/.NET%20Core/badge.svg?branch=master)">
    <img src="https://github.com/Relfos/TOMB/workflows/.NET%20Core/badge.svg?branch=master">
  </a>
  <a href="https://github.com/phantasma-io/PhantasmaChain/blob/master/LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-blue.svg">
  </a>
</p>


## Supported features

- Smart contracts and Non-contract Scripts (eg: transactions, raw invokes)
- Numbers, strings, bools, timestamps, addresses, hashes
- Constants
- Enums
- Global and local variables
- Array indexing
- Bitshifting and logical operators
- Contract constructors, methods and triggers
- Contract public methods
- Return values
- Collections (Maps and lists)
- Generic types
- If ... Else
- While ... and Do ... While loops
- Switch .. case
- Break and Continue
- Throw Exceptions
- Uninitialized globals validation
- Custom events
- Interop and Contract calls
- Inline asm
- Structs
- Import libraries (Runtime, Leaderboard, Token, etc)
- Comments (single and multi line)
- Contract tasks
- ABI generation

## Planned features

- For.. Loops
- Try .. Catch
- More...
- Warnings
- Debugger support

## Feature Requests

- Call a function from anywhere in the code
- Create Classes that can be manipulated
- Change Struct values of an instanciated struct without needing to recreated
- Fix if's and else's and add else if, also add && and ||
- Better support for Arrays, methods like, Array.shuffle() | Array.push() | Array.add() | Array.pop() | Array.shift()
- Better Math Library, implement methods like, Math.Ceil() | Math.floor()
- Multiple file support (Before compiling it, to make the code easier to write.)
- Implement a null types

## Literals

Different data types are recognized by the compiler.

| Type  | Example |
| ------------- | ------------- |
| Number  | 123  |
| Decimal<X>  | 0.123  | Where X is the number of maximum decimal places
| Bool  | false  |
| String  | "hello"  |
| Timestamp  | no literal support, use either Time.now or Time.unix  |
| Byte array  | 0xFAFAFA2423424 |
| Address | @P2K6p3VzyRhxqHE2KcNV2B3QjVrv5ekvWPZLevteDoBQTzA or @null|
| Hash  | #E3FE7BB73996CF7057913BD916F1B07AC0EAB4916DF3BCBDC221829F5CBEA9AF |
| Compiler macro   | $SOMETHING |

## Available libraries

The following libraries can be imported into a contract.

### Call
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Call.interop(...:Generic) | Any | TODO|
| Call.contract(method:String, ...:Generic) | Any | This is used to call another contract with a specified method.|
| Call.method(...:Generic) | Any | To call a method inside the contract, but instead of using "this.methodName()"|

### Runtime
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Runtime.expect(condition:Bool, error:String) | None | To check if the condition is true, else returns the error, and the code below, won't be executed.|
| Runtime.log(message:String) | None | To log a message.|
| Runtime.isWitness(address:Address) | Bool | Check if is they the owner of that given Address.|
| Runtime.isTrigger() | Bool | Returns true if a trigger and false otherwise.|
| Runtime.transactionHash() | Hash | TODO|
| Runtime.deployContract(from:Address, contract:Module) | None | TODO|
| Runtime.upgradeContract(from:Address, contract:Module) | None | TODO|
| Runtime.gasTarget() | Address | TODO|
| Runtime.context() | String | TODO|
| Runtime.previousContext() | String | TODO|

### Math
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Math.min(a:Number, b:Number) | Number | Returns smallest of two numbers|
| Math.max(a:Number, b:Number) | Number | Returns largest of two numbers|

### Token
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Token.create(from:Address, symbol:String, name:String, maxSupply:Number, decimals:Number, flags:Number, script:Bytes, abi:Bytes) | None | Method used to create a new token.|
| Token.exists(symbol:String) | Bool | Returns true if the token exists and false otherwise.|
| Token.getDecimals(symbol:String) | Number | Returns the number of decimals of the token.|
| Token.getFlags(symbol:String) | Enum<TokenFlag> | Returns an Enum with the TokenFlag of the token.|
| Token.transfer(from:Address, to:Address, symbol:String, amount:Number) | None | Transfers tokens from one Address, to another address with a specific symbol and the desired amount.|
| Token.transferAll(from:Address, to:Address, symbol:String) | None | Transfer all tokens from one Address, to another address with a specific symbol.|
| Token.mint(from:Address, to:Address, symbol:String, amount:Number) | None | Mints tokens from one Address, to another address with a specific symbol and the desired amount.|
| Token.write(from:Address, symbol:String, tokenID:Number, ram:Any) | None | Updates the Token/NFT RAM with the given RAM.|
| Token.burn(from:Address, symbol:String, amount:Number) | None | Burn tokens from the given address, given symbol and the desired amount.|
| Token.swap(targetChain:String, source:Address, destination:Address, symbol:String, amount:Number) | None | TODO|
| Token.getBalance(from:Address, symbol:String) | Number | Returns the token balance of the specified address.|
| Token.isMinter(address:Address, symbol:String) | Bool | Returns true if the token is a Minter and false otherwise.|

### NFT
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| NFT.transfer(from:Address, to:Address, symbol:String, id:Number) | None | Transfer an NFT from one address to another, by the nftID and symbol.|
| NFT.mint(from:Address, to:Address, symbol:String, rom:Any, ram:Any, seriesID:Number) | None | Mint an NFT from one address to another, with the specific ROM and RAM, and the seriesID.|
| NFT.write(from:Address, symbol:String, tokenID:Number, ram:Any) | None | Write NFT is to update the RAM inside the NFT by the nftID.|
| NFT.burn(from:Address, symbol:String, id:Number) | None | Burn the nft by the NFTID.|
| NFT.infuse(from:Address, symbol:String, id:Number, infuseSymbol:String, infuseValue:Number) | None | Infuse the NFT with other tokens/NFT with a given amount.|
| NFT.createSeries(from:Address, symbol:String, seriesID:Number, maxSupply:Number, mode:Enum<TokenSeries>, nft:Module) | None | Creates a series of NFTs.|
| NFT.readROM<T>(symbol:String, id:Number) | T | Returns the ROM by the NFTID.|
| NFT.readRAM<T>(symbol:String, id:Number) | T | Returns the RAM by the NFTID.|

### Account
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Account.getName(from:Address) | String | TODO|
| Account.getLastActivity(from:Address) | Timestamp | TODO|
| Account.registerName(target:Address, name:String) | None | TODO|
| Account.unregisterName(target:Address) | None | TODO|
| Account.registerScript(target:Address, script:Bytes, abiBytes:Bytes) | None | TODO|
| Account.hasScript(address:Address) | Bool | TODO|
| Account.lookUpAddress(target:Address) | String | TODO|
| Account.lookUpScript(target:Address) | Bytes | TODO|
| Account.lookUpABI(target:Address) | Bytes | TODO|
| Account.lookUpName(name:String) | Address | TODO|
| Account.migrate(from:Address, target:Address) | None | TODO|

### Organization
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Organization.create(from:Address, id:String, name:String, script:Bytes) | None | TODO|
| Organization.addMember(from:Address, name:String, target:Address) | None | TODO|

### Oracle
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Oracle.read(url:String) | None | TODO|
| Oracle.price(symbol:String) | None | Retruns the price of the given symbol.|
| Oracle.quote(baseSymbol:String, quoteSymbol:String, amount:Number) | None | Returns the price converted to the given quote symbol with the given amount.|

### Storage
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Storage.read(contract:String, field:String, type:Number) | Any | TODO|
| Storage.write(field:String, value:Any) | None | TODO|
| Storage.delete(field:String) | None | TODO|
| Storage.calculateStorageSizeForStake(stakeAmount:Number) | Number | TODO|
| Storage.createFile(target:Address, fileName:String, fileSize:Number, contentMerkle:Bytes, encryptionContent:Bytes) | None | TODO|
| Storage.hasFile(target:Address, hash:Hash) | Bool | TODO|
| Storage.addFile(from:Address, target:Address, archiveHash:Hash) | None | TODO|
| Storage.deleteFile(from:Address, targetHash:Hash) | None | TODO|
| Storage.hasPermission(externalAddr:Address, target:Address) | Bool | TODO|
| Storage.addPermission(from:Address, externalAddr:Address) | None | TODO|
| Storage.deletePermission(from:Address, externalAddr:Address) | None | TODO|
| Storage.migratePermission(target:Address, oldAddr:Address, newAddr:Address) | None | TODO|
| Storage.migrate(from:Address, target:Address) | None | TODO|
| Storage.getUsedSpace(from:Address) | Number | TODO|
| Storage.getAvailableSpace(from:Address) | Number | TODO|
| Storage.GetUsedDataQuota(address:Address) | Number | TODO|
| Storage.writeData(target:Address, key:Bytes, value:Bytes) | None | TODO|
| Storage.deleteData(target:Address, key:Bytes) | None | TODO|

### Array
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Array.get(array:Any, index:Number) | Generic<0> | Returns the element of an array at the given index.|
| Array.set(array:Any, index:Number, value:Generic<0>) | None | Set the element of an array at the given index with the given value.|
| Array.remove(array:Any, index:Number) | None | Removes the element of an array at the given index.|
| Array.clear(array:Any) | None | Clears all the Array entries.|
| Array.count(array:Any) | Number | Returns the number of elements in the Array.|

### Utils
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Utils.contractAddress(name:String) | Address | TODO|

### Leaderboard
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Leaderboard.create(from:Address, boardName:String, capacity:Number) | None | To create a new leaderboard by the given address with a board name and a given capacity.|
| Leaderboard.getAddress(boardName:String, index:Number) | Address | Returns the address of the leaderboard, by the given board name and index.|
| Leaderboard.getScoreByIndex(boardName:String, index:Number) | Number | Returns the score that position, by the given board name and index.|
| Leaderboard.getScoreByAddress(boardName:String, target:Address) | Number | Returns the score of the address, by the given board name and the target address.|
| Leaderboard.getSize(boardName:String) | Number | Returns the size of the Leaderboard, by the given board name.|
| Leaderboard.insert(from:Address, target:Address, boardName:String, score:Number) | None | To insert a score into the Leaderboard, by the target address, board name and score.|
| Leaderboard.reset(from:Address, boardName:String) | None | To reset the Leaderboard, by the address and board name.|

### Market
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Market.sell(from:Address, baseSymbol:String, quoteSymbol:String, tokenID:Number, price:Number, endDate:Timestamp) | None | To sell an NFT, by the tokenID.|
| Market.buy(from:Address, symbol:String, tokenID:Number) | None | To buy an NFT, by the tokenID.|
| Market.cancel(symbol:String, tokenID:Number) | None | To cancel a Sell.|
| Market.hasAuction(symbol:String, tokenID:Number) | Bool | Returns true if has an auction for the given tokenID.|
| Market.bid(from:Address, symbol:String, tokenID:Number, price:Number, buyingFee:Number, buyingFeeAddress:Address) | None | To bid for the given tokenID.|
| Market.listToken(from:Address, baseSymbol:String, quoteSymbol:String, tokenID:Number, price:Number, endPrice:Number, startDate:Timestamp, endDate:Timestamp, extensionPeriod:Number, typeAuction:Number, listingFee:Number, listingFeeAddress:Address) | None | To list the token by the TokenID.|
| Market.editAuction(from:Address, baseSymbol:String, quoteSymbol:String, tokenID:Number, price:Number, endPrice:Number, startDate:Timestamp, endDate:Timestamp, extensionPeriod:Number) | None | To edit the auction for the given tokenID.|
 
### Crowdsale
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Crowdsale.create(from:Address, name:String, SaleFlags flags, startDate:Timestamp, endDate:Timestamp, sellSymbol:String, receiveSymbol:String, price:Number, globalSoftCap:Number, globalHardCap:Number, userSoftCap:Number, userHardCap:Number) | Hash | Returns a Hash of the sale created.|
| Crowdsale.isSaleActive(saleHash:Hash) | bool | Returns true if the sale is active, false otherwise.|
| Crowdsale.GetSaleParticipants(saleHash:Hash) | Address[] | Returns an Array of the addressess in by the saleHash.|
| Crowdsale.getSaleWhitelists(saleHash:Hash) | Address[] | Retruns the list of addresses whitelisted for the sale, by the saleHash.|
| Crowdsale.isWhitelisted(saleHash:Hash, address:Address) | Bool | Returns true if the user is whitelisted for the sale, false otherwise.|
| Crowdsale.addToWhitelist(saleHash:Hash, target:Address) | None | To add a Address to the participate in the sale, by the saleHash and target address.|
| Crowdsale.removeFromWhitelist(saleHash:Hash, target:Address) | None | To remove a Address from the participate in the sale, by the saleHash and target address.|
| Crowdsale.getPurchasedAmount(saleHash:Hash, address:Address) | Number | Returns the Purchased amount.|
| Crowdsale.getSoldAmount(saleHash:Hash) | Number | Returns the amount that the sale has been sold.|
| Crowdsale.purchase(from:Address, saleHash:Hash, quoteSymbol:string, quoteAmount:Number) | None | To purchase the sale.|
| Crowdsale.closeSale(from:Address, saleHash:Hash) | None | To close a given saleHash.|
| Crowdsale.getLatestSaleHash() | Hash | Returns the last saleHash.|
| Crowdsale.EditSalePrice(saleHash:Hash, price:Number) | None | To edit the sale price by the saleHash.|

### Stake
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Stake.getMasterThreshold() | Number | TODO|
| Stake.isMaster(address:Address) | bool | TODO|
| Stake.getMasterCount() | Number | TODO|
| Stake.getClaimMasterCount(claimDate:Timestamp) | Number | TODO|
| Stake.getMasterClaimDate(claimDistance:Number) | Timestamp | TODO|
| Stake.getMasterDate(target:Address) | Timestamp | TODO|
| Stake.getMasterClaimDateFromReference(claimDistance:Number, referenceTime:Timestamp) | Timestamp | TODO|
| Stake.getMasterRewards(address:Address) | Number | TODO|
| Stake.migrate(from:Address, to:Address) | None | TODO|
| Stake.masterClaim(from:Address) | None | TODO|
| Stake.stake(from:Address, stakeAmount:Number) | None | TODO|
| Stake.unstake(from:Address, unstakeAmount:Number) | None | TODO|
| Stake.getTimeBeforeUnstake(from:Address) | Number | TODO|
| Stake.getStakeTimestamp(from:Address) | Timestamp | TODO|
| Stake.getUnclaimed(from:Address) | Number | TODO|
| Stake.claim(from:Address, stakeAddress:Address) | None | TODO|
| Stake.getStake(address:Address) | Number | TODO|
| Stake.getStorageStake(address:Address) | Number | TODO|
| Stake.fuelToStake(fuelAmount:Number) | Number | TODO|
| Stake.stakeToFuel(stakeAmount:Number) | Number | TODO|
| Stake.getAddressVotingPower(address:Address) | Number | TODO|
| Stake.updateRate() | None | TODO|
| Stake.getRate() | Number | TODO|

### Governance
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Governance.hasName(name:String) | bool | TODO|
| Governance.gasValue(name:String) | bool | TODO|
| Governance.createValue(name:String, initial:Number, serializedConstraints:Bytes) | None | TODO|
| Governance.getValue(name:String) | Number | TODO|
| Governance.setValue(name:String, value:Number) | None | TODO|

### Relay
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Relay.getBalance(from:Address) | Number | TODO|
| Relay.getIndex(from:Address, to:Address) | Number | TODO|
| Relay.getTopUpAddress(from:Address) | Address | TODO|
| Relay.openChannel(from:Address, publicKey:Bytes) | None | TODO|
| Relay.getKey(from:Address) | Bytes | TODO|
| Relay.topUpChannel(from:Address, count:Number) | None | TODO|
| Relay.settleChannel(receipt:RelayReceipt) | None | TODO|

### Mail
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Mail.pushMessage(from:Address, target:Address, archiveHash:Hash) | None | To push a message to the target user mailbox.|
| Mail.domainExists(domainName:String) | Bool | Returns true if the specified domain exists, false otherwise.|
| Mail.registerDomain(from:Address, domainName:String) | None | To register a domain, from an address and a domain name.|
| Mail.unregisterDomain(domainName:String) | None | To unregister a domain name.|
| Mail.migrateDomain(domainName:String, target:Address) | None | To migrate a domain to a new Address.|
| Mail.joinDomain(from:Address, domainName:String) | None | To a user join a domain.|
| Mail.leaveDomain(from:Address, domainName:String) | None | To a user leave a domain.|
| Mail.getUserDomain(target:Address) | String | To the the user domain.|

### Time
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Time.now() | Timestamp | Returns the current time.|
| Time.unix(value:Number) | Timestamp | Returns the time for the given value.|

### Task
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Task.start(method:Method, from:Address, frequency:Number, mode:Enum<TaskMode>, gasLimit:Number) | Task | Start the task by method name, from the given address and frequency(timestamp), the TaskMode and the gasLimit.|
| Task.stop(task:Address) | None | Stop the task method.|
| Task.current() | Task | Returns teh current task method.|

### UID
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| UID.generate() | Number | Returns a unique identifier.|

### Map
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Map.get(key:Generic) | Generic | Returns the value by the given key.|
| Map.set(key:Generic, value:Generic) | None | Set's the value to the specified key.|
| Map.remove(key:Generic) | None | Removes the key from the map.|
| Map.clear() | None | Clears all the Map entries.|
| Map.count() | Number | Returns the number of entries in the Map.|
| Map.has(key:Generic) | Bool | Returns if the key exists in the Map.|

### List
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| List.get(index:Number) | Generic | Returns the element at the given index.|
| List.add(value:Generic) | None | To add the value to the list.|
| List.replace(index:Number, value:Generic) | None | Replaces the value at the given index.|
| List.remove(index:Number) | None | Removes from the list at a given index.|
| List.count() | Number | Returns the number of entries in the List.|
| List.clear() | None | Clears all the entries in the List.|

### String
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| String.toBytes(target:String) | Bytes | To convert a given string into a byte array, and returns it.|
| String.length(target:String) | Number | Returns the length of the string.|
| String.substr(target:String, index:Number, length:Number) | String | Returns the substring of the given string at an index and a length.|
| String.toArray(target:String) | Array<Number> | To convert the String into an Array of Numbers that represent each Character in the String.|
| String.fromArray(target:Array<Number>) | String | To convert a given Array<Number> into a String, each number represents a Character.|

### Decimal
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Decimal.decimals(target:Any) | Number | Returns the number of decimals of the given target.|
| Decimal.convert(decimalPlaces:Number, value:Number) | Number | Returns the converted value of the given decimal places.|

### Enum
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Enum.isSet(target:Enum<>, flag:Enum<>) | Bool | Returns true if the enum is set, false otherwise.|

### Address
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Address.isNull(target:Address) | Bool | Returns true if the address is null, false otherwise.|
| Address.isUser(target:Address) | Bool | Returns true if the address is a user, false otherwise.|
| Address.isSystem(target:Address) | Bool | Returns true if the address is a System address, false otherwise.|
| Address.isInterop(target:Address) | Bool | Returns true if the address is an Internal Operation, false otherwise.|

### Module
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Module.getScript(target:Module) | Bytes | TODO|
| Module.getABI(target:Module) | Bytes | TODO|

### Format
| Method | Return type | Description|
| ------------- | ------------- |------------- |
| Format.decimals(value:Number, symbol:String) | String | Returns a string with the value formated to the given symbol.|
| Format.symbol(symbol:String) | String | Returns a string representation of the given symbol.|
| Format.account(address:Address) | String | Returns a String with the account formated to print.|

### Available macros

| Macro  | Description |
| ------------- | ------------- |
| $THIS_ADDRESS  | The address of the current contract  |
| $THIS_SYMBOL  | The symbol of the current token  |
| $TYPE_OF  | The type of the argument  |

## Exception support

Currently it is possible to throw exceptions with a string message.<br/>
Runtime.expect() can also be used as an alternative way of throwing exceptions based on a condition.<br/>
More work will include support for other data types and support for try..catch.<br/>

```c#
...
throw "something happened";
...
}
```


# Examples

## Simple Sum
Simple contract that sums two numbers and returns the result

```c#
contract test {
	public sum(a:number, b:number):number
	{
		return a + b;
	}
}
```

## Conditions
Like most programming languages, it is possible to do conditional branching use if statement.<br/>
Logic operators supported include and, or and xor.<br/>

```c#
contract test {
	public isEvenAndPositive(n:number):bool
	{
		if (n>0 and n%2==0)
		{
			return true;
		}
		else {
			return false;
		}
	}
}
```

## Switch case
Simple contract that sums two numbers and returns the result

```c#
contract test {
    public check(x:number): string {
        switch (x) {
            case 0: return "zero";
            case 1: return "one";
            case 2: return "two";
            default: return "other";
        }                  
	}
}
 ```

## Simple Counter
Simple contract that implements a global counter (that can be incremented by anyone who calls the contract).<br/>
Note that any global variable that is not generic must be initialized in the contract constructor.<br/>

```c#
contract test {
	global counter: number;

	constructor(owner:address)
	{
		counter:= 0;
	}

	public increment()
	{
		if (counter < 0){
			throw "invalid state";
		}
		counter += 1;
	}
}
```

## Counter per Address
Another contract that implements a counter, this time unique per user address.<br/>
Showcases how to validate that a transaction was done by user possessing private keys to 'from' address

```c#
contract test {
	import Runtime;
	import Map;

	global counters: storage_map<address, number>;

	public increment(from:address)
	{
		Runtime.expect(Runtime.isWitness(from), "witness failed");
		local temp: number;
		temp := counters.get(from);
		temp += 1;
		counters.set(from, temp);
	}
}
```

## Strings
Simple contract that shows how to use strings and builtin type methods, string.length() in this specific case.<br/>

```c#
contract test {
	global val: string;

	constructor(owner:address)
	{
		val := "hello";
		val += " world";
	}

	public getLength():number
	{
		return val.length();
	}
}
```

## Decimals
There is compiler support for decimal numbers.<br/>
Note that internally those are converted to Number types in fixed point format.

```c#
contract test {
	global val: decimal<4>; // the number between <> is the number of decimal places

	constructor(owner:address)
	{
		val := 2.1425;
	}

	public getValue():number
	{
		return val; // this will return 21425, which is the previous value in fixed point format
	}

	public getDecimals():number
	{
		return val.decimals(); // this returns 4 as result
	}

	public sum(other:decimal<4>):number
	{
		return val + other;
	}

}
```

## Enums
There is compiler support for enumerated value types, that map directly to the Phantasma VM enum type.<br/>

```c#
// NOTE - like other custom types, it is declared outside the scope of a contract
enum MyEnum { A = 0, B = 1, C = 2}
// if the numbers are sequential, it is ok to ommit them, eg:
//enum MyEnum { A, B, C}

contract test {
	global state: MyEnum;

	constructor(owner:address)
	{
		state := MyEnum.B;
	}

	public getValue():MyEnum
	{
		return state;
	}		
}
```

## Map support
The compiler supports generic types, including maps.<br/>
Maps are one of the few types that don't have to initialized in the constructor.<br/>

```c#
contract test {
	global my_state: storage_map<address, number>;

	constructor(owner:address)
	{
		my_state.set(owner, 42);
	}

	public getState(target:address):number
	{
		return my_state.get(target);
	}
}
```

## String manipulation
The compiler supports generic types, including maps.<br/>
Maps are one of the few types that don't have to initialized in the constructor.<br/>

```c#
contract test {
	import Array;
	
	public toUpper(s:string):string 
	{        
		local my_array: array<number>;		
		
		// extract chars from string into an array
		my_array := s.toArray();	
		
		local length :number := Array.length(my_array);
		local idx :number := 0;
		
		while (idx < length) {
			local ch : number := my_array[idx];
			
			if (ch >= 97) {
				if (ch <= 122) {				
					my_array[idx] := ch - 32; 
				}
			}
						
			idx += 1;
		}
				
		// convert the array back into a unicode string
		local result:string := String.fromArray(my_array); 
		return result;
	}	
}
```

## Random numbers
It is possible to generate pseudo random numbers, and also to control the generation seed.<br/>
If a seed is not specified, then the current transaction hash will be used as seed, if available.<br/>

```c#
contract test {
	import Random;

	global my_state: number;

	constructor(owner:address)
	{
		Random.seed(16676869); // optionally we can specify a seed, this will make the next sequence of random numbers to be deterministic
		my_state := mutateState();
	}

	public mutateState():number
	{
		my_state := Random.generate() % 1024; // Use modulus operator to constrain the random number to a specific range
		return my_state;
	}
}
```

## Transfer Tokens
A contract that takes a payment in tokens from a user.<br/>
Showcases how to transfer tokens and how to use macro $THIS_ADDRESS to obtain address of the contract.

```c#
contract test {
	import Runtime;
	import Token;

	public paySomething(from:address, quantity:number)
	{
		Runtime.expect(Runtime.isWitness(from), "witness failed");

		local price: number := 10;
		price *= quantity;

		local thisAddr:address := $THIS_ADDRESS;
		Token.transfer(from, thisAddr, "SOUL", price);

		// TODO after payment give something to 'from' address
	}
}
```

## Token Flags
There are also some builtin enums, like TokenFlags.<br/>

```c#
contract test {
	import Runtime;
	import Token;

	public paySomething(from:address, amount:number, symbol:string)
	{
		Runtime.expect(Runtime.isWitness(from), "witness failed");

		local flags:TokenFlags := Token.getFlags(symbol);

		if (flags.isSet(TokenFlags.Fungible)) {
			local thisAddr:address := $THIS_ADDRESS;
			Token.transfer(from, thisAddr, "SOUL", price);
		}
	}
}
```

## Validation
Runtime.Expect offers a clean way to validate conditions.<br/>
The developer of a smart contract must be very careful to ensure that no exploits are possible due to missing validations.<br/>

```c#
contract test {
	import Runtime;

	public doSomething(from:address)  {
		Runtime.expect(from.isUser(), "expected user address"); // makes sure the address is of 'user' type
		Runtime.expect(Runtime.isWitness(from), "invalid witness"); // makes sure the transaction was signed by 'from' address
		Runtime.expect(Runtime.gasTarget() == $THIS_ADDRESS, "invalid donation"); // makes sure the transaction fees are donated to this contract

		// actually do something after passing all validation
	}
}
```

## Call method
Showcases how a contract method can call other methods.<br/>
If a method is declared private, it can't be called by anyone except the actual contract that implements it.

```c#
contract test {
	private sum(a:number, b:number) {
		return a + b;
	}

	public calculatePrice(x:number): number
	{		
		local price: number := 10;
		price := this.sum(price, x); // here we use 'this' for calling another method

		return price;
	}
}
```


## Scripts
A script is something that can be used either for a transaction or for an API invokeScript call.<br/>
This example showcases a simple script with one argument, that calls a contract.<br/>
Note that for scripts with arguments, for them to run properly you will have to push them into the stack before.

```c#
script startup {

	import Call;

	code(target:address) {
		local temp:number := 50000;
		Call.contract("Stake", "Unstake", target, temp);
	}
}
```

## Deploy contract script 

This example showcases a script that deploys a token contract.

```c#
token GHOST {
...
}

script deploy {

    import Token;
    import Module;

    code() {
        local maxSupply:number := 50000;
        local decimals:number := 1;
		local flags:TokenFlags := TokenFlags.None;
        Token.create(@P2KAkQRrL62zYvb5198CHBLiKHKr4bJvAG7aXwV69rtbeSz, "GHOST",  "Ghost Token", maxSupply, decimals, flags, Module.getScript(GHOST),  Module.getABI(GHOST));
    }
}
```

## Minting Script
This example showcases a script that mints an custom NFT.<br/>

```c#
struct my_rom_data {
	name:string;
	counter:number;
}

script token_minter {

	import Token;

	code(source:address, target:address) {
		local rom_data:my_rom_data := Struct.my_rom_data("hello", 123);
		NFT.mint(source, target, "LOL", rom_data, "ram_can_be_anything");
	}
}
```

## Inline asm
Inline asm allows to write assembly code that is then inserted and merged into the rest of the code.<br/>
This feature is useful as an workaround for missing features in the compiler.

```c#
script startup {

	import Call;

	code() {
		local temp:string;
		asm {
			LOAD $temp "hello"
		}
	}
}
```

## Custom events 1
Showcases how a contract can declare and emit custom events.

```c#
contract test {
	event MyPayment:number = "{address} paid {data}"; // here we use a short-form description

	public paySomething(from:address, x:number)
	{		
		Runtime.expect(Runtime.isWitness(from), "witness failed");

		local price: number := 10;
		local thisAddr:address := $THIS_ADDRESS;
		Token.transfer(from, thisAddr, "SOUL", price);

		emit MyPayment(from, price);
	}
}
```

## Custom events 2
A more complex version of the previous example, showcasing custom description scripts.

```c#
description payment_event {

	code(from:address, amount:number): string {
		local result:string := "";
		result += from;
		result += " paid ";
		result += amount;
		return result;
	}
}

contract test {
	event MyPayment:number = payment_event; // here we use a short-form declaration

	// everything else would be same as previous example
}
```

## Custom events 3
A yet more complex version of the previous examples, showcasing custom description scripts and also struct declarations.

```c#
struct my_event_data {
	amount:number;
	symbol:string;
}

description payment_event {

	code(from:address, data:my_event_data): string {
		local result:string := "";
		result += from;
		result += " paid ";
		result += data.amount;
		result += " ";
		result += data.symbol;
		return result;
	}
}

contract test {
	event MyPayment:my_event_data = payment_event; // here we use a short-form declaration

	// everything else would be same as previous examples
}
```

## Triggers 1
A contract example showcasing triggers.<br/>
In this example, this account will only accept transfers of KCAL and reject anything else.

```c#
contract test {

	trigger onReceive(from:address, symbol:string, amount:number)
	{
		if (symbol != "KCAL") {
			throw "can't receive asset: " + symbol;
		}

		return;
	}
}
```

## Triggers 2
Another contract example showcasing triggers.<br/>
In this example, any asset sent to this account will be auto-converted into SOUL.

```c#
contract test {

	trigger onReceive(from:address, symbol:string, amount:number)
	{
		if (symbol != "SOUL") {
			Call.contract("Swap", "SwapTokens", from, symbol, "SOUL", amount);
		}

		return;
	}
}
```

## Method variables
It is possible to use methods as variables.<br/>

```c#
contract test {

	import Runtime;
	import Map;

	global _counter:number;

	global _callMap: storage_map<address, method<address>>;

	constructor(owner:address)
	{
		_counter := 0;
	}

	public registerUser(from:address, amount:number)
	{
		local target: method<address>;

		if (amount > 10) {
			target := incCounter;
		}
		else {
			target := decCounter;
		}

		_callMap.set(from, target);
	}

	public callUser(from:address) {
		local target: method<address> := _callMap.get(from);

		Call.method(target, from);
	}

	private incCounter(target:address) {
		_counter += 1;
	}

	private subCounter(target:address) {
		_counter -= 1;
	}
}
```

## Tasks
A task allows a contract method to run periodically without user intervention.<br/>
Tasks can't have parameters, however you can use Task.current() along with a global Map to associate custom user data to each task.<br/>

```c#
contract test {
	import Time;
	import Task;

	global victory:bool;
	global deadline:timestamp;

	constructor(owner:address) {
		victory := false;
		time := Time.now() + time.hours(2);
		Task.start(checkResult, owner, 0, TaskFrequency.Always, 999);
	}

	task checkResult()  {
		if (victory) {
			break;
		}

		local now: timestamp := Time.now();

		if (time >= deadline) {
			break;
		}

		continue;
	}

	public win(from:address)
	{
		victory := true;
	}
}
```



## Multi-signature
Yet another contract example showcasing triggers.<br/>
In this example, a multi-signature account is implemented.

```c#
contract test {

	global owners: storage_list<address>;

	constructor(owner:address)
	{
		owners.add(owner);
	}

	private validateSignatures() {
		local index:number := 0;
		local count:number := owners.count();

		while (index < count) {
			local addr:address := owners.get(index);
			if (!Runtime.isWitness(addr)) {
				throw "missing signature of "+addr;
			}
		}
	}

	public isOwner(target:address):bool {
		local index:number := 0;
		local count:number := owners.count();

		while (index < count) {
			local addr:address := owners.get(index);
			if (addr == target) {
				return true;
			}
		}

		return false;
	}

	public addOwner(target:address) {
		Runtime.expect(!isOwner(target), "already is owner");
		validateSignatures();
		owners.add(target);
	}

	trigger onSend(from:address, symbol:string, amount:number)
	{
		validateSignatures();
	}
}
```

## Fungible Token
Showcases how to implement a fungible token (eg: the Phantasma equivalent to an Ethereum ERC20).

```c#
token DOG { // this defines the token symbol as DOG
	import Runtime;

	property name:string = "Dog Token";

	property isFungible: bool = true;

	property isDivisible: bool = true;
	property decimals:number = 8; // required only if isDivisible is true
	
	property isTransferable: bool = true;
	property isBurnable: bool = true;
	
	property isFinite: bool = false;
	//property maxSupply: number = 1000000; // required only if isFinite is true
	
	global _admin: address;
	
	constructor(owner:address)	{
       _admin := owner;
	}

	// allows the token to be upgraded later, remove this trigger if you want a imutable fungible token
	trigger onUpgrade(from:address) 
	{
		Runtime.expect(Runtime.isWitness(_admin), "witness failed");
		return;
	}
	
	// its possible to also add more triggers, custom methods etc
}
```

## NFTs
Showcases how to implement an NFT, showcasing all details including ROM, RAM and token series.

When creating an NFT, they must have 4 default properties implemented and they're:
- ```name```, returns the name of the NFT
- ```description```, returns the descriptions of the NFT
- ```imageURL```, returns the image URL of the NFT
- ```infoURL```, returns the info URL of the NFT

```c#
struct luchador_rom
{
	genes:bytes;
	name:string;
}

struct luchador_ram
{
	experience:number;
	level:number;
}

struct item_rom
{
	kind:number;
	quality:number;
}

struct item_ram
{
	power:number;
	level:number;
}

token NACHO {
	global _owner: address;

	const LUCHADOR_SERIES: number = 1;
	const LUCHADOR_SUPPLY: number = 100000;

	const ITEM_SERIES: number = 2;
	const ITEM_SUPPLY: number = 500000;

	property name: string = "Nachomen";

	property isBurnable: bool = true;
	property isFinite: bool = true;
	property isFungible: bool = false;
	property maxSupply: number = LUCHADOR_SUPPLY + ITEM_SUPPLY;

	nft luchador<luchador_rom, luchador_ram> {

		property name: string {
			return _ROM.name;
		}

		property description: string {
			return "Luchador with level " + _RAM.level;
		}

		property imageURL: string {
			return "https://nacho.men/img/luchador/"+ _tokenID;
		}

		property infoURL: string {
			return "https://nacho.men/api/luchador/"+ _tokenID;
		}
	}

	nft item<item_rom, item_ram> {

		property name: string {
			switch (_ROM.kind)
			{
				case 1: return "Potion";
				case 2: return "Gloves";
				default: return "Item #" + _ROM.kind;
			}
		}

		property description: string {
			return "Item level " + _RAM.level;
		}

		property imageURL: string {
			return "https://nacho.men/img/item/"+ _tokenID;
		}

		property infoURL: string {
			return "https://nacho.men/api/item/"+ _tokenID;
		}
	}	

	constructor (addr:address) {
		_owner := addr;
		// at least one token series must exist, here we create 2 series
		// they don't have to be created in the constructor though, can be created later
		NFT.createSeries(_owner, $THIS_SYMBOL, LUCHADOR_SERIES, LUCHADOR_SUPPLY, TokenSeries.Unique, luchador);
		NFT.createSeries(_owner, $THIS_SYMBOL, ITEM_SERIES, ITEM_SUPPLY, TokenSeries.Unique, item);
	}
}

```

## Call contract from another contract
Example showcasing calling contract storage directly from another contract.<br/>
Basic version where another storage map is called, and this value is incremented and stored in another contract storage.<br/>

```c#
contract test {

	import Map;
	import Storage;
	import Call;

	global counters: storage_map<number, number>;

	private getContractCount(tokenId:number):number {
	
		local count:number := Call.interop<number>("Map.Get",  "OTHERCONTRACT", "_storageMap", tokenId, $TYPE_OF(number));
		return count;
		
	}

	public updateCount(tokenID:number) {
	
		local contractCounter:number := this.getContractCount(tokenID);
		contractCounter += 1;
		counters.set(tokenID, contractCounter);
		
	}

	public getCount(tokenID:number):number {
	
		local temp:number := counters.get(tokenID);
		return temp;
		
	}
}
```

# More documentation
Check our official <a href="https://docs.phantasma.io/#tomb-supported_features">Phantasma documentation</a> for more info about developing with Phantasma Chain.