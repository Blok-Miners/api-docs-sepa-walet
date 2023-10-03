API Documentation for Crypto On Ramp Off Ramp:-

Authentication

Dev can put in api key in “headers.X-api-key”// Need to discuss with Sepa
Rate Limit

{
      ttl: 60000,
      limit: 10,
}

This the default value in nest js but it can be changed according to requirement

Logs and Alerts:- // Need to discuss with Sepa or Kibana, sentry

 Endpoints

List and describe the available API endpoints. For each endpoint, include the following information:

1. Endpoint: `/Generate-Master-Key`

Note:- Need to discuss with Sepa about KMS

#Method: `Post`

*Description:* Generate Tenant master key for all operation of On ramp Off ramp Db.

*Parameters:*

{
	Blockchain Network
}

*Request Example:*

let config = {
 method: 'post',
 url: 'http://localhost:5000/Generate-Master-Key,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 },
 data : {
	  Blockchain: Ethereum Mainnet
        }
};

*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
{
data:{
MasterKey : ‘0x..’
}
}

*Response Codes:*

- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters.
- `403 Forbidden: Blockchain not supported
- `500 Internal Server Error`: Server error.


2. Endpoint: `/Generate-Api-key`

#Method: `Post`

*Description: ‘Create an api key for api cunsumptions’.

*Parameters:*

{
	MasterKey: ‘0x….’
}

*Request Example:*

let config = {
 method: 'post',
 url: 'http://localhost:5000/Generate-Api-key,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 },
 data : {
	  MasterKey: ‘0x….’
        }
};


*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : {
	  Api Key: ‘344366…’
        }
};


*Response Codes:*

- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters.
- `404 Not Found`: Key not found.
- `500 Internal Server Error`: Server error.

3. Endpoint: `/create-wallet`

# Method: `POST`

*Description:* Create a new wallet.

*Parameters:*

- type : CUSTODIAL / NON CUSTODIAL.
- Master Key: ‘0x..’
- asset:  Asset Id
- index number (custodial)(Not required): (total Number of virtual address generated from one master key -1),

*Request Example:*

let config = {
 method: 'post',
 url: 'http://localhost:5000/create-wallet,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 },
 data : {
	type: “CUSTODIAL”
	masterKey: ‘0x….’,
asset:  Asset Id       // Refer api 4,5,
index number (custodial): (total Number of virtual address generated from one master key -1)
        }
};


*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : {
	  walletId: ‘344366…’
	  walletAddress: 
        }
};

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters.
- `404 Not Found`: (Key not found|| Asset Not Found || index number).
- `500 Internal Server Error`: Server error.






4. Endpoint: `/add-asset`

# Method: `POST`

*Description:* Add a new asset to the database.

*Parameters:*

- blockchain : Ethereum. // Need to map blockchains with their ids in database,
- Asset Name : ‘USDT’,
- Contract Address: ‘0x..’

*Request Example:*

let config = {
 method: 'post',
 url: 'http://localhost:5000/create-wallet,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 },
 data : {
	blockchain: “ethereum”
	AssetName: ‘ETH’,
Contract Address: ‘0x..’
        }
};


*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : {
	  AssetId: ‘344366…’
        }
};

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters.
- `403 Forbidden: Blockchain not supported
- `500 Internal Server Error`: Server error.





5 . Endpoint: `/get-all-asset`

# Method: `Get`

*Description:* Fetch all assets from Database.

*Request Example:*

let config = {
 method: get,
 url: 'http://localhost:5000/get-all-asset,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 }};


*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : [{
	  AssetId: ‘344366…’,
	  Asset Name: ‘ETH’
	  Blockchain: “ethereum”
          }] 

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters.
- `404 Not Found: Resource Not found 
- `500 Internal Server Error`: Server error.



6. Endpoint: `/get-asset-by-id`

# Method: `GET`

*Description:* Add a new asset to the database.

*Query Parameters:*

- blockchain : Ethereum. // Need to map blockchains with their ids in database
- Asset Id : ‘00e5niew798’

*Request Example:*

let config = {
 method: ‘get’,
 url: 'http://localhost:5000/create-wallet?blockchain=ethereum&assetId=0EH5934NO8,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 }};


*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : {
	  AssetId: ‘344366…’,
	  Asset Name: ‘ETH’
	  Blockchain: “ethereum”
        }
};

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters.
- `403 Forbidden: Blockchain not supported,
- `404 Not Found: Resource Not found 
- `500 Internal Server Error`: Server error.



1 Webhook URL Endpoint: `/deposit`

# Method: `POST`
*Description:* Sync Database with the blockchain when the user deposits some currencies.
*Parameters:*

walletAddress: “0x….”,
Retries :  0 to 5(can be customized),
Assetname: “ETH”,
Blockchain: “ethereum”
Deposit amount: 59 (In ether valu not the wei)(It Also can be negative because for non custodial wallet a withdraw can happen outside from our application)


*Request Example:*

let config = {
 method: 'post',
 url: 'http://localhost:5000/deposit,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 },
 data : {
	walletAddress: “0x….”,
	Retries :  0 to 5(can be customized),
	Assetname: “ETH”,
	Blockchain: “ethereum”
	Deposit amount: 59 (In ether valu not the wei)(It Also can be negative because for non custodial wallet a withdraw can happen outside from our application)
};

*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json

Note:- If not 200 status then there will be a retry from the event listener, Also this endpoints is only for to update the database

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters.
- `403 Forbidden: Asset Id not supported
- `500 Internal Server Error`: Server error.



7. Endpoint: `/withdraw-asset`

# Method: `POST`

*Description:* Withdraw assets from Custodial wallets

*Parameters:*

-AssetId : “0ejy43n30935”
-MasterKey: “0x.. ” 
- Amount: 6743(in ether value)
-receiverAddress: “0x.. .. ”

*Request Example:*

let config = {
 method: 'post',
 url: 'http://localhost:5000/withdraw-asset,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 },
 data : {
	AssetId : “0ejy43n30935”,
MasterKey: “0x.. ” ,
Amount: 6743(in ether value)
receiverAddress: “0x.. .. ”
        }
};


*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : {
	  Transaction Hash: “0x.. … ”
        }
};

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters./ Wallet does not have enough balance to perform the transaction // wallet does not 
- `404 Not Found: Key not Found
- `500 Internal Server Error`: Server error.

8. Endpoint: `/transfer`

# Method: `POST`

*Description:* 
*Parameters:*

-AssetId : “0ejy43n30935”
-MasterKey: “0x.. ” 
- Amount: 6743(in ether value)
-receiverWalletId: “0kho438kjby ”

*Request Example:*

let config = {
 method: 'post',
 url: 'http://localhost:5000/transfer,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 },
 data : {
	AssetId : “0ejy43n30935”,
MasterKey: “0x.. ” ,
Amount: 6743(in ether value)
receiverWalletId: “0kho438kjby ”
        }
};


*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : {
	  Transaction Hash: “0xqeh083uu4obu9 ” // Database level
        }
};

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters./ Wallet does not have enough balance to perform the transaction
- `404 Not Found: Key not Found
- `500 Internal Server Error`: Server error.



9. Endpoint: `/exchange`

Note:- Rates for exchange will be taken from third party application like kareken

# Method: `POST`

*Description:* 
*Parameters:*

-AssetId : “0ejy43n30935”
-MasterKey: “0x.. ” 
- Amount: 6743(in ether value)
-receivingAssetId: “0kho438kjby93”

*Request Example:*

let config = {
 method: 'post',
 url: 'http://localhost:5000/exchange,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 },
 data : {
	AssetId : “0ejy43n30935”,
MasterKey: “0x.. ”,
Amount: 6743(in ether value),
receivingAssetId: “0kho438kjby93”
        }
};


*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : {
	  Transaction Hash: “0xqeh083uu4obu9 ” // Database level,
	  Order Id : “09732jg9ydsf32”
        }
};

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters./ Wallet does not have enough balance to perform the transaction,
- `403 Forbidden: Asset id / receiving asset id not supported,
- `404 Not Found: Key not Found
- `500 Internal Server Error`: Server error.





10. Endpoint: `/getBalance`

# Method: `GET`

*Description:* Gets the balance of a particular token or coin for a user
*Parameters:*

-walletId : “0ejy43n30935”

*Request Example:*

let config = {
 method: ‘get’,
 url: 'http://localhost:5000/getBalance?walletId=0ejy43n30935,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 }

*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : {
	  Balance: 405.93 
        };

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters.
- `404 Not Found: wallet not Found
- `500 Internal Server Error`: Server error.




11. Endpoint: `/getWalletTransactions`

# Method: `POST`

*Description:* fetch all the transaction made by a wallet
*Parameters:*

-walletId : “0ejy43n30935”

*Request Example:*

let config = {
 method: 'post',
 url: 'http://localhost:5000/getWalletTransactions,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 },
 data : {
	walletId : “0ejy43n30935”,
};


*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : {
	  Transactions: [{
		transactionId: “0xhuew08345”
		UserWallet : “hd7932n090”,
		transactionType: “TRANSFER”,
		ReceivingWallet: “hshdohasf2347”,
		Amount: “435”,
		AssetId: {
			Id: “09u239b88y32”,
			Blockchain: “ethereum”,
			assetName: “USDT”
}
}]
        };

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters.
- `404 Not Found: wallet not Found
- `500 Internal Server Error`: Server error.





12. Endpoint: `/getTransactionById`

# Method: `POST`

*Description:* fetch the transaction by it’s transactionId
*Parameters:*

-transactionId : “0xhuew08345”

*Request Example:*

let config = {
 method: 'post',
 url: 'http://localhost:5000/getTransactionById,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 },
 data : {
	transactionId : “0xhuew08345”
};


*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : {
	transactionId: “0xhuew08345”
	UserWallet : “hd7932n090”,
	transactionType: “TRANSFER”,
	ReceivingWallet: “hshdohasf2347”,
	Amount: “435”,
	AssetId: {
		Id: “09u239b88y32”,
		Blockchain: “ethereum”,
		assetName: “USDT”
}
        };

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters.
- `404 Not Found: transaction not Found
- `500 Internal Server Error`: Server error.

13. Endpoint: `/getWalletOrders`

# Method: `POST`

*Description:* Fetch all the order happened from a user wallet
*Parameters:*

-walletId : “0ejy43n30935”

*Request Example:*

let config = {
 method: 'post',
 url: 'http://localhost:5000/getWalletTransactions,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 },
 data : {
	walletId : “0ejy43n30935”,
};


*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : {
	  Orders: [{
		orderId: “wrr09p3443j0”
		transactionId: “0xhuewai0932”
		senderWallet : “hd7932n090”,
		transactionType: “BUY”,
		ReceivingWallet: “hshdohasf2347”,
		Amount: “435”,
		Pair : “USDT/USDC”,
		AssetId1: {
			Id: “09u239b88y32”,
			Blockchain: “ethereum”,
			assetName: “USDT”
},
AssetId2: {
			Id: “90345jb893”,
			Blockchain: “ethereum”,
			assetName: “USDC”
}
}]
        };

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters.
- `404 Not Found: wallet not Found
- `500 Internal Server Error`: Server error.





14. Endpoint: `/getOrderById`

# Method: `POST`

*Description:*  Fetch the order by particular ID
*Parameters:*

-orderId : “wrr09p3443j0”

*Request Example:*

let config = {
 method: 'post',
 url: 'http://localhost:5000/getTransactionById,
 headers: {
   'Content-Type': 'application/json',
   X-api-key:  Api_Key
 },
 data : {
 	orderId : “wrr09p3443j0”
};


*Response Example:*

json
HTTP/1.1 200 OK
Content-Type: application/json
data : {
	orderId: “wrr09p3443j0”
transactionId: “0xhuewai0932”
	senderWallet : “hd7932n090”,
	transactionType: “BUY”,
	ReceivingWallet: “hshdohasf2347”,
	Amount: “435”,
	Pair : “USDT/USDC”,
	AssetId1: {
		Id: “09u239b88y32”,
		Blockchain: “ethereum”,
		assetName: “USDT”
},
AssetId2: {
		Id: “90345jb893”,
		Blockchain: “ethereum”,
		assetName: “USDC”
}
        };

*Response Codes:*
- `200 OK`: Success, returns the requested data.
- `400 Bad Request`: Invalid parameters or missing required parameters.
- `404 Not Found: order not Found
- `500 Internal Server Error`: Server error.
