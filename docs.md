## API Documentation for Crypto On-Ramp/Off-Ramp

### Authentication

Developers can include the API key in the request headers using the `X-api-key` field. The specific authentication mechanism should be discussed with Sepa.

### Rate Limit

The default rate limit values in NestJS are as follows, but they can be adjusted according to requirements:

- Time-to-Live (TTL): 60,000 milliseconds (1 minute)
- Limit: 10 requests per minute

### Logs and Alerts

Logging and alerting mechanisms should be discussed with Sepa or integrated with tools like Kibana and Sentry.

---

### Endpoints

1. **Endpoint: `/Generate-Master-Key`**

   - **Method:** `POST`
   - **Description:** Generate Tenant master key for all operations of the On-Ramp/Off-Ramp Database.
   - **Parameters:**
     - Blockchain Network (Specify Blockchain)
   - **Request Example:**
   
     ```json
     let config = {
       method: 'POST',
       url: 'http://localhost:5000/Generate-Master-Key',
       headers: {
         'Content-Type': 'application/json',
         'X-api-key':  'Api_Key'
       },
       data: {
         "Blockchain": "Ethereum Mainnet"
       }
     };
     ```
   - **Response Example:**
   
     ```json
     HTTP/1.1 200 OK
     Content-Type: application/json
     {
       "data": {
         "MasterKey": "0x.."
       }
     }
     ```
   - **Response Codes:**
     - `200 OK`: Success, returns the requested data.
     - `400 Bad Request`: Invalid parameters or missing required parameters.
     - `403 Forbidden`: Blockchain not supported.
     - `500 Internal Server Error`: Server error.

2. **Endpoint: `/Generate-Api-key`**

   - **Method:** `POST`
   - **Description:** Create an API key for API consumption.
   - **Parameters:**
     - Master Key: "0x..."
   - **Request Example:**
   
     ```json
     let config = {
       method: 'POST',
       url: 'http://localhost:5000/Generate-Api-key',
       headers: {
         'Content-Type': 'application/json',
         'X-api-key': 'Api_Key'
       },
       data: {
         "MasterKey": "0x..."
       }
     };
     ```
   - **Response Example:**
   
     ```json
     HTTP/1.1 200 OK
     Content-Type: application/json
     {
       "data": {
         "Api Key": "344366..."
       }
     }
     ```
   - **Response Codes:**
     - `200 OK`: Success, returns the requested data.
     - `400 Bad Request`: Invalid parameters or missing required parameters.
     - `404 Not Found`: Key not found.
     - `500 Internal Server Error`: Server error.

3. **Endpoint: `/create-wallet`**

   - **Method:** `POST`
   - **Description:** Create a new wallet.
   - **Parameters:**
     - Type: CUSTODIAL / NON CUSTODIAL
     - Master Key: "0x.."
     - Asset: Asset Id (Refer to API 4, 5)
     - Index Number (Custodial, Not required): Total number of virtual addresses generated from one master key - 1
   - **Request Example:**
   
     ```json
     let config = {
       method: 'POST',
       url: 'http://localhost:5000/create-wallet',
       headers: {
         'Content-Type': 'application/json',
         'X-api-key': 'Api_Key'
       },
       data: {
         "type": "CUSTODIAL",
         "masterKey": "0x...",
         "asset": "Asset Id",
         "index number (custodial)": "Total Number of virtual address generated from one master key - 1"
       }
     };
     ```
   - **Response Example:**
   
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
   - **Response Codes:**
     - `200 OK`: Success, returns the requested data.
     - `400 Bad Request`: Invalid parameters or missing required parameters.
     - `404 Not Found`: Key not found, Asset Not Found, index number not found.
     - `500 Internal Server Error`: Server error.

4. **Endpoint: `/add-asset`**

   - **Method:** `POST`
   - **Description:** Add a new asset to the database.
   - **Parameters:**
     - Blockchain: Ethereum
     - Asset Name: "USDT"
     - Contract Address: "0x.."
   - **Request Example:**
   
     ```json
     let config = {
       method: 'POST',
       url: 'http://localhost:5000/add-asset',
       headers: {
         'Content-Type': 'application/json',
         'X-api-key': 'Api_Key'
       },
       data: {
         "blockchain": "ethereum",
         "AssetName": "ETH",
         "Contract Address": "0x.."
       }
     };
     ```
   - **Response Example:**
   
     ```json
     HTTP/1.1 200 OK
     Content-Type: application/json
     {
       "data": {
         "AssetId": "344366..."
       }
     }
     ```
   - **Response Codes:**
     - `200 OK`: Success, returns the requested data.
     - `400 Bad Request`: Invalid parameters or missing required parameters.
     - `403 Forbidden`: Blockchain not supported.
     - `500 Internal Server Error`: Server error.

5. **Endpoint: `/get-all-asset`**

   - **Method:** `GET`
   - **Description:** Fetch all assets from the Database.
   - **Request Example:**
   
     ```json
     let config = {
       method: 'GET',
       url: 'http://localhost:5000/get-all-asset',
       headers: {
         'Content-Type': 'application/json',
         'X-api-key': 'Api_Key'
       }
     };
     ```
   - **Response Example:**
   
     ```json
     HTTP/1.1 200 OK
     Content-Type: application/json
     {
       "data": [
         {
           "AssetId": "344366...",
           "Asset Name": "ETH",
           "Blockchain": "ethereum"
         }
       ]
     }
     ```
   - **Response Codes:**
     - `200 OK`: Success, returns the requested data.
     - `400 Bad Request`: Invalid parameters or missing required parameters.
     - `404 Not Found`: Resource not found.
     - `500 Internal Server Error`: Server error.

6. **Endpoint: `/get-asset-by-id`**

   - **Method:** `GET`
   - **Description:** Retrieve an asset from the database.
   - **Query Parameters:**
     - Blockchain: Ethereum
     - Asset Id: "00e5niew

798"
   - **Request Example:**
   
     ```json
     let config = {
       method: 'GET',
       url: 'http://localhost:5000/get-asset-by-id?blockchain=ethereum&assetId=00e5niew798',
       headers: {
         'Content-Type': 'application/json',
         'X-api-key': 'Api_Key'
       }
     };
     ```
   - **Response Example:**
   
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
   - **Response Codes:**
     - `200 OK`: Success, returns the requested data.
     - `400 Bad Request`: Invalid parameters or missing required parameters.
     - `403 Forbidden`: Blockchain not supported.
     - `404 Not Found`: Resource not found.
     - `500 Internal Server Error`: Server error.

7. **Endpoint: `/deposit`**

   - **Method:** `POST`
   - **Description:** Sync the Database with the blockchain when the user deposits some currencies.
   - **Parameters:**
     - walletAddress: "0x..."
     - Retries: 0 to 5 (customizable)
     - Assetname: "ETH"
     - Blockchain: "ethereum"
     - Deposit amount: 59 (in ether value, not wei) (It can also be negative for non-custodial wallets)
   - **Request Example:**
   
     ```json
     let config = {
       method: 'POST',
       url: 'http://localhost:5000/deposit',
       headers: {
         'Content-Type': 'application/json',
         'X-api-key': 'Api_Key'
       },
       data: {
         "walletAddress": "0x...",
         "Retries": 0, // Customize this
         "Assetname": "ETH",
         "Blockchain": "ethereum",
         "Deposit amount": 59
       }
     };
     ```
   - **Response Example:**
   
     ```json
     HTTP/1.1 200 OK
     Content-Type: application/json
     ```
     Note: If not a 200 status, there will be a retry from the event listener. This endpoint is for updating the database.
   - **Response Codes:**
     - `200 OK`: Success, returns the requested data.
     - `400 Bad Request`: Invalid parameters or missing required parameters.
     - `403 Forbidden`: Asset Id not supported.
     - `500 Internal Server Error`: Server error.

8. **Endpoint: `/withdraw-asset`**

   - **Method:** `POST`
   - **Description:** Withdraw assets from Custodial wallets.
   - **Parameters:**
     - AssetId: "0ejy43n30935"
     - MasterKey: "0x.."
     - Amount: 6743 (in ether value)
     - receiverAddress: "0x.. .."
   - **Request Example:**
   
     ```json
     let config = {
       method: 'POST',
       url: 'http://localhost:5000/withdraw-asset',
       headers: {
         'Content-Type': 'application/json',
         'X-api-key': 'Api_Key'
       },
       data: {
         "AssetId": "0ejy43n30935",
         "MasterKey": "0x..",
         "Amount": 6743,
         "receiverAddress": "0x.. .."
       }
     };
     ```
   - **Response Example:**
   
     ```json
     HTTP/1.1 200 OK
     Content-Type: application/json
     {
       "data": {
         "Transaction Hash": "0x.. ..."
       }
     }
     ```
   - **Response Codes:**
     - `200 OK`: Success, returns the requested data.
     - `400 Bad Request`: Invalid parameters or missing required parameters. Wallet does not have enough balance to perform the transaction.
     - `404 Not Found`: Key not found.
     - `500 Internal Server Error`: Server error.

9. **Endpoint: `/transfer`**

   - **Method:** `POST`
   - **Description:** Transfer assets between wallets.
   - **Parameters:**
     - AssetId: "0ejy43n30935"
     - MasterKey: "0x.."
     - Amount: 6743 (in ether value)
     - receiverWalletId: "0kho438kjby"
   - **Request Example:**
   
     ```json
     let config = {
       method: 'POST',
       url: 'http://localhost:5000/transfer',
       headers: {
         'Content-Type': 'application/json',
         'X-api-key': 'Api_Key'
       },
       data: {
         "AssetId": "0ejy43n30935",
         "MasterKey": "0x..",
         "Amount": 6743,
         "receiverWalletId": "0kho438kjby"
       }
     };
     ```
   - **Response Example:**
   
     ```json
     HTTP/1.1 200 OK
     Content-Type: application/json
     {
       "data": {
         "Transaction Hash": "0xqeh083uu4obu9" // Database level
       }
     }
     ```
   - **Response Codes:**
     - `200 OK`: Success, returns the requested data.
     - `400 Bad Request`: Invalid parameters or missing required parameters. Wallet does not have enough balance to perform the transaction.
     - `404 Not Found`: Key not found.
     - `500 Internal Server Error`: Server error.

10. **Endpoint: `/exchange`**

    - **Method:** `POST`
    - **Description:** Perform an exchange between assets. Rates for exchange will be taken from a third-party application like Kareken.
    - **Parameters:**
      - AssetId: "0ejy43n30935"
      - MasterKey: "0x.."
      - Amount: 6743 (in ether value)
      - receivingAssetId: "0kho438kjby93"
    - **Request Example:**
    
      ```json
      let config = {
        method: 'POST',
        url: 'http://localhost:5000/exchange',
        headers: {
          'Content-Type': 'application/json',
          'X-api-key': 'Api_Key'
        },
        data: {
          "AssetId": "0ejy43n30935",
          "MasterKey": "0x..",
          "Amount": 6743,
          "receivingAssetId": "0kho438kjby93"
        }
      };
      ```
    - **Response Example:**
    
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
    - **Response Codes:**
      - `200 OK`: Success, returns the requested data.
      - `400 Bad Request`: Invalid parameters or missing required parameters. Wallet

 does not have enough balance to perform the transaction.
      - `403 Forbidden`: Asset id / receiving asset id not supported.
      - `404 Not Found`: Key not found.
      - `500 Internal Server Error`: Server error.

That concludes the API documentation for Crypto On-Ramp/Off-Ramp. Please note that this documentation is provided for reference, and you may need to adapt it to your specific API implementation and documentation style.

