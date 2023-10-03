Here's the formatted API documentation for the Crypto On-Ramp/Off-Ramp service:

# Authentication

Developers can put an API key in the request headers using `X-api-key`. Further discussions are needed with Sepa regarding authentication.

# Rate Limit

- Default Rate Limit:
  - Time to Live (ttl): 60000 milliseconds (60 seconds)
  - Request limit: 10 requests
  - Note: These default values can be adjusted according to specific requirements.

# Logs and Alerts

Logs and alerts integration details need to be discussed with Sepa or using tools like Kibana and Sentry.

# Endpoints

## 1. Generate Master Key

- **Endpoint**: `/Generate-Master-Key`
- **Method**: `POST`
- **Description**: Generate Tenant master key for all operations of On-Ramp/Off-Ramp DB.
- **Parameters**:
  - Blockchain Network
- **Request Example**:
  ```javascript
  let config = {
    method: 'POST',
    url: 'http://localhost:5000/Generate-Master-Key',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    },
    data: {
      Blockchain: 'Ethereum Mainnet'
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "MasterKey": "0x..."
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the requested data.
  - `400 Bad Request`: Invalid parameters or missing required parameters.
  - `403 Forbidden`: Blockchain not supported.
  - `500 Internal Server Error`: Server error.

## 2. Generate API Key

- **Endpoint**: `/Generate-Api-key`
- **Method**: `POST`
- **Description**: Create an API key for API consumption.
- **Parameters**:
  - Master Key: '0x...'
- **Request Example**:
  ```javascript
  let config = {
    method: 'POST',
    url: 'http://localhost:5000/Generate-Api-key',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    },
    data: {
      MasterKey: '0x...'
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "Api Key": "344366..."
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the requested data.
  - `400 Bad Request`: Invalid parameters or missing required parameters.
  - `404 Not Found`: Key not found.
  - `500 Internal Server Error`: Server error.

## 3. Create Wallet

- **Endpoint**: `/create-wallet`
- **Method**: `POST`
- **Description**: Create a new wallet.
- **Parameters**:
  - Type: CUSTODIAL / NON CUSTODIAL.
  - Master Key: '0x..'
  - Asset: Asset Id
  - Index number (custodial) (Not required): Total Number of virtual addresses generated from one master key - 1.
- **Request Example**:
  ```javascript
  let config = {
    method: 'POST',
    url: 'http://localhost:5000/create-wallet',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    },
    data: {
      type: "CUSTODIAL",
      masterKey: '0x...',
      asset: 'Asset Id',
      indexNumberCustodial: 'Total Number of virtual addresses generated'
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "walletId": "344366...",
      "walletAddress": "..."
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the requested data.
  - `400 Bad Request`: Invalid parameters or missing required parameters.
  - `404 Not Found`: Key not found, Asset Not Found, index number not found.
  - `500 Internal Server Error`: Server error.

## 4. Add Asset

- **Endpoint**: `/add-asset`
- **Method**: `POST`
- **Description**: Add a new asset to the database.
- **Parameters**:
  - Blockchain: Ethereum.
  - Asset Name: 'USDT'.
  - Contract Address: '0x..'.
- **Request Example**:
  ```javascript
  let config = {
    method: 'POST',
    url: 'http://localhost:5000/create-wallet',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    },
    data: {
      blockchain: "ethereum",
      assetName: 'ETH',
      contractAddress: '0x..'
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "AssetId": "344366..."
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the requested data.
  - `400 Bad Request`: Invalid parameters or missing required parameters.
  - `403 Forbidden`: Blockchain not supported.
  - `500 Internal Server Error`: Server error.

## 5. Get All Asset

- **Endpoint**: `/get-all-asset`
- **Method**: `GET`
- **Description**: Fetch all assets from the Database.
- **Request Example**:
  ```javascript
  let config = {
    method: 'GET',
    url: 'http://localhost:5000/get-all-asset',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": [{
      "AssetId": "344366...",
      "Asset Name": "ETH",
      "Blockchain": "ethereum"
    }]
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the requested data.
  - `400 Bad Request`: Invalid parameters or missing required parameters.
  - `404 Not Found`: Resource not found.
  - `500 Internal Server Error`: Server error.

## 6. Get Asset by ID

- **Endpoint**: `/get-asset-by-id`
- **Method**: `GET`
- **Description**: Fetch an asset from the database by its ID.
- **Query Parameters**:
  - Blockchain: Ethereum.
  - Asset Id: '00e5niew798'.
- **Request Example**:
  ```javascript
  let config = {
    method: 'GET',
    url: 'http://localhost:5000/get-asset-by-id?blockchain=ethereum&assetId=0EH5934NO8',
    headers: {
      'Content-Type': '

application/json',
      'X-api-key': 'Api_Key'
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "AssetId": "344366...",
      "Asset Name": "ETH",
      "Blockchain": "ethereum"
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the requested data.
  - `400 Bad Request`: Invalid parameters or missing required parameters.
  - `403 Forbidden`: Blockchain not supported.
  - `404 Not Found`: Resource not found.
  - `500 Internal Server Error`: Server error.

## 7. Deposit

- **Endpoint**: `/deposit`
- **Method**: `POST`
- **Description**: Sync the database with the blockchain when a user deposits some currencies.
- **Parameters**:
  - Wallet Address: "0x..."
  - Retries: 0 to 5 (can be customized)
  - Asset Name: "ETH"
  - Blockchain: "ethereum"
  - Deposit Amount: 59 (In ether value, not wei). It can also be negative because for non-custodial wallets, withdrawals can happen outside the application.
- **Request Example**:
  ```javascript
  let config = {
    method: 'POST',
    url: 'http://localhost:5000/deposit',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    },
    data: {
      walletAddress: "0x...",
      retries: 0,
      assetName: "ETH",
      blockchain: "ethereum",
      depositAmount: 59
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  ```
  - Note: If the status code is not 200, there will be a retry from the event listener. This endpoint is only for updating the database.
- **Response Codes**:
  - `200 OK`: Success, no specific response data.
  - `400 Bad Request`: Invalid parameters or missing required parameters.
  - `403 Forbidden`: Asset ID not supported.
  - `500 Internal Server Error`: Server error.

## 8. Withdraw Asset

- **Endpoint**: `/withdraw-asset`
- **Method**: `POST`
- **Description**: Withdraw assets from custodial wallets.
- **Parameters**:
  - Asset ID: "0ejy43n30935"
  - Master Key: "0x.."
  - Amount: 6743 (In ether value)
  - Receiver Address: "0x.. .."
- **Request Example**:
  ```javascript
  let config = {
    method: 'POST',
    url: 'http://localhost:5000/withdraw-asset',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    },
    data: {
      assetId: "0ejy43n30935",
      masterKey: "0x..",
      amount: 6743,
      receiverAddress: "0x.. .."
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "Transaction Hash": "0x.. ..."
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the transaction hash.
  - `400 Bad Request`: Invalid parameters or missing required parameters, insufficient balance.
  - `404 Not Found`: Key not found.
  - `500 Internal Server Error`: Server error.

## 9. Transfer

- **Endpoint**: `/transfer`
- **Method**: `POST`
- **Description**: Transfer assets between wallets.
- **Parameters**:
  - Asset ID: "0ejy43n30935"
  - Master Key: "0x.."
  - Amount: 6743 (In ether value)
  - Receiver Wallet ID: "0kho438kjby"
- **Request Example**:
  ```javascript
  let config = {
    method: 'POST',
    url: 'http://localhost:5000/transfer',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    },
    data: {
      assetId: "0ejy43n30935",
      masterKey: "0x..",
      amount: 6743,
      receiverWalletId: "0kho438kjby"
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "Transaction Hash": "0xqeh083uu4obu9" // Database level
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the transaction hash.
  - `400 Bad Request`: Invalid parameters or missing required parameters, insufficient balance.
  - `404 Not Found`: Key not found.
  - `500 Internal Server Error`: Server error.

## 10. Exchange

- **Endpoint**: `/exchange`
- **Method**: `POST`
- **Description**: Exchange one asset for another.
- **Parameters**:
  - Asset ID: "0ejy43n30935"
  - Master Key: "0x.."
  - Amount: 6743 (In ether value)
  - Receiving Asset ID: "0kho438kjby93"
- **Request Example**:
  ```javascript
  let config = {
    method: 'POST',
    url: 'http://localhost:5000/exchange',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    },
    data: {
      assetId: "0ejy43n30935",
      masterKey: "0x..",
      amount: 6743,
      receivingAssetId: "0kho438kjby93"
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "Transaction Hash": "0xqeh083uu4obu9", // Database level
      "Order Id": "09732jg9ydsf32"
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the transaction hash and order ID.
  - `400 Bad Request`: Invalid parameters or missing required parameters, insufficient balance.
  - `403 Forbidden`: Asset ID / receiving asset ID not supported.
  - `404 Not Found`: Key not found.
  - `500 Internal Server Error`: Server error.

## 11. Get Balance

- **Endpoint**: `/getBalance`
- **Method**: `GET`
- **Description**: Get the balance of a particular token or coin for a user.
- **Parameters**:
  - Wallet ID: "0ejy43n30935"
- **Request Example**:
  ```javascript
  let config = {
    method: 'GET',
    url: 'http://localhost:5000/getBalance?walletId=0ejy43n30935',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "Balance": 405.93
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the balance.
  - `400 Bad Request`: Invalid parameters or missing required parameters.
  - `404 Not Found`: Wallet not found.
  - `500 Internal Server Error`: Server error.

## 12. Get Wallet Transactions

- **Endpoint**: `/getWalletTransactions`
- **Method**: `POST`
- **Description**: Fetch all the transactions made by a wallet.
- **Parameters**:
  - Wallet ID: "0ejy43n30935"
- **Request Example**:
  ```javascript
  let config = {
    method: 'POST',
    url: 'http://localhost:5000/getWalletTransactions',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    },
    data: {
      walletId: "0ejy43n30935"
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "Transactions": [{
        "transactionId": "0xhuew08345",
        "UserWallet": "hd7932n090",
        "transactionType": "TRANSFER",
        "ReceivingWallet": "hshdohasf2347",
        "Amount": "435",
        "AssetId": {
          "Id": "09u239b88y32",
          "Blockchain": "ethereum",
          "assetName": "USDT"
        }
      }]
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the list of transactions.
  - `400 Bad Request`: Invalid parameters or missing required parameters.
  - `404 Not Found`: Wallet not found.
  - `500 Internal Server Error`: Server error.

## 13. Get Transaction by ID

- **Endpoint**: `/getTransactionById`
- **Method**: `POST`
- **Description**: Fetch a transaction by its transaction ID.
- **Parameters**:
  - Transaction ID: "0xhuew08345"
- **Request Example**:
  ```javascript
  let config = {
    method: 'POST',
    url: 'http://localhost:5000/getTransactionById',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    },
    data: {
      transactionId: "0xhuew08345"
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "transactionId": "0xhuew08345",
      "UserWallet": "hd7932n090",
      "transactionType": "TRANSFER",
      "ReceivingWallet": "hshdohasf2347",
      "Amount": "435",
      "AssetId": {
        "Id": "09u239b88y32",
        "Blockchain": "ethereum",
        "assetName": "USDT"
      }
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the transaction details.
  - `400 Bad Request`: Invalid parameters or missing required parameters.
  - `404 Not Found`: Transaction not found.
  - `500 Internal Server Error`: Server error.

## 14. Get Wallet Orders

- **Endpoint**: `/getWalletOrders`
- **Method**: `POST`
- **Description**: Fetch all the orders made from a user's wallet.
- **Parameters**:
  - Wallet ID: "0ejy43n30935"
- **Request Example**:
  ```javascript
  let config = {
    method: 'POST',
    url: 'http://localhost:5000/getWalletOrders',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    },
    data: {
      walletId: "0ejy43n30935"
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "Orders": [{
        "orderId": "wrr09p3443j0",
        "transactionId": "0xhuewai0932",
        "senderWallet": "hd7932n090",
        "transactionType": "BUY",
        "ReceivingWallet": "hshdohasf2347",
        "Amount": "435",
        "Pair": "USDT/USDC",
        "AssetId1": {
          "Id": "09u239b88y32",
          "Blockchain": "ethereum",
          "assetName": "USDT"
        },
        "AssetId2": {
          "Id": "90345jb893",
          "Blockchain": "ethereum",
          "assetName": "USDC"
        }
      }]
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the list of orders.
  - `400 Bad Request`: Invalid parameters or missing required parameters.
  - `404 Not Found`: Wallet not found.
  - `500 Internal Server Error`: Server error.

## 15. Get Order by ID

- **Endpoint**: `/getOrderById`
- **Method**: `POST`
- **Description**: Fetch an order by its particular ID.
- **Parameters**:
  - Order ID: "wrr09p3443j0"
- **Request Example**:
  ```javascript
  let config = {
    method: 'POST',
    url: 'http://localhost:5000/getOrderById',
    headers: {
      'Content-Type': 'application/json',
      'X-api-key': 'Api_Key'
    },
    data: {
      orderId: "wrr09p3443j0"
    }
  };
  ```
- **Response Example**:
  ```json
  HTTP/1.1 200 OK
  Content-Type: application/json
  {
    "data": {
      "orderId": "wrr09p3443j0",
      "transactionId": "0xhuewai0932",
      "senderWallet": "hd7932n090",
      "transactionType": "BUY",
      "ReceivingWallet": "hshdohasf2347",
      "Amount": "435",
      "Pair": "USDT/USDC",
      "AssetId1": {
        "Id": "09u239b88y32",
        "Blockchain": "ethereum",
        "assetName": "USDT"
      },
      "AssetId2": {
        "Id": "90345jb893",
        "Blockchain": "ethereum",
        "assetName": "USDC"
      }
    }
  }
  ```
- **Response Codes**:
  - `200 OK`: Success, returns the order details.
  - `400 Bad Request`: Invalid parameters or missing required parameters.
  - `404 Not Found`: Order not found.
  - `500 Internal Server Error`: Server error.
