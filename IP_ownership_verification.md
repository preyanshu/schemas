
### **Schema Proposal: Blockchain-based Intellectual Property (IP) Ownership Verification (Using IPFS and Ethereum)**

#### **Data Source Name**

IPFS (InterPlanetary File System) and Ethereum are decentralized technologies that allow users to store and verify intellectual property ownership securely on the blockchain. IPFS allows for decentralized storage, while Ethereum's smart contracts can be used to manage ownership, licensing, and transfer of intellectual property rights.

#### **API Endpoint URL**

-   **IPFS Upload URL**: `POST https://ipfs.infura.io:5001/api/v0/add`
-   **Ethereum Smart Contract Endpoint (for ownership verification)**: `GET https://api.etherscan.io/api?module=contract&action=getabi&address={contract_address}`

#### **Purpose**

This schema validates the ownership and licensing of intellectual property stored on IPFS and recorded on Ethereum. The schema allows creators, innovators, and businesses to prove that they are the rightful owners of intellectual property by verifying its digital fingerprint on the blockchain.

#### **Sample JSON Response (IPFS and Ethereum Integration)**

```json
`{
  "product_id": "digital_art_12345",
  "creator": "0x8f0e7d130b00424c2f31adfeea6fd26a443b905d", 
  "ipfs_hash": "QmXxU8sytujUw9c8UM6Xb3yRhz9vwGr9h7oJ1Vq7dchfky", 
  "contract_address": "0x2345ab24c234bc234c9837cb134dcbd042736374", 
  "ownership_verified": true,
  "license_type": "Exclusive",
  "license_start_date": "2024-01-01",
  "license_end_date": "2025-01-01",
  "creator_ethereum_address": "0x8f0e7d130b00424c2f31adfeea6fd26a443b905d",
  "creator_signed_message": "Ownership verified through Ethereum smart contract and IPFS storage."
}` 
```

#### **Technical Breakdown**

This schema is designed to verify intellectual property (IP) ownership and licensing using IPFS and Ethereum. The key validation conditions are:

-   **IPFS Hash**: The `ipfs_hash` field must point to a valid file stored on the IPFS network, representing the digital work (e.g., an artwork, software code, or document). The IPFS file is uniquely identifiable using the hash.
-   **Ethereum Ownership**: The ownership of the digital asset is recorded on Ethereum using a smart contract. The smart contract address and Ethereum account must be checked to verify ownership.
-   **License Verification**: The schema also verifies if the intellectual property has been licensed, including the type of license (e.g., exclusive, non-exclusive) and the licensing period.

#### **Key Use Cases**

-   **NFT Marketplace**: This schema can be used to verify the ownership and licensing status of NFTs (Non-Fungible Tokens) that represent digital art, music, and other creative works.
-   **Copyright Management**: Creators can use this schema to prove their ownership of digital assets and manage the licensing and transfer of IP rights.
-   **Patent and Trademark Verification**: Businesses and creators can use this schema to verify ownership of patents or trademarks represented as digital assets on the blockchain.

#### **Schema Code**

```json
`{
  "issuer": "IPFS & Ethereum",
  "desc": "Verifies the ownership and licensing of digital assets stored on IPFS and recorded on Ethereum",
  "website": "https://www.infura.io",
  "APIs": [
    {
      "host": "ipfs.infura.io",
      "intercept": {
        "url": "/api/v0/add",
        "method": "POST"
      },
      "assert": [
        {
          "key": "ipfs_hash",
          "operation": "exists"
        }
      ]
    },
    {
      "host": "api.etherscan.io",
      "intercept": {
        "url": "/api",
        "method": "GET"
      },
      "assert": [
        {
          "key": "ownership_verified",
          "value": "true",
          "operation": "="
        }
      ]
    }
  ],
  "HRCondition": [
    "The intellectual property must be correctly recorded and verified on both IPFS and Ethereum smart contract."
  ],
  "tips": {
    "message": "Ensure the digital asset is stored securely on IPFS and linked with an Ethereum smart contract for ownership verification."
  },
  "category": "Intellectual Property",
  "id": "0xIPFSEthereumOwnershipVerifier"
}` 
```

#### **Demo/Test Case**

-   **Scenario**: A creator wants to prove that they are the original owner of a digital art piece (e.g., a 3D model) and that the work is licensed exclusively to a business for one year.
    -   The creator uploads the digital artwork to IPFS and receives an IPFS hash: `QmXxU8sytujUw9c8UM6Xb3yRhz9vwGr9h7oJ1Vq7dchfky`.
    -   The artwork is then associated with a smart contract on Ethereum, and the ownership of the artwork is recorded.
    -   The creator verifies the ownership of the artwork by checking the Ethereum smart contract, which shows that the creator is listed as the owner and the IPFS hash matches the artwork.
    -   The schema validation ensures that the IPFS hash exists and that the ownership is recorded on Ethereum, confirming that the creator is the rightful owner and that the artwork is licensed for a period of time.

#### **Real-World Use Case**

This schema could be implemented on a decentralized marketplace for digital assets, where buyers and sellers can verify ownership and licensing details of digital art or other IP. Additionally, this schema could be integrated into platforms that offer intellectual property management solutions, allowing businesses and creators to securely track, license, and transfer ownership of their digital products. It would also be helpful in ensuring that NFT creators are the rightful owners of their creations before they are sold.