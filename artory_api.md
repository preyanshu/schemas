
### **Schema Proposal: Digital Art Ownership and Provenance Verification (Using Artory API)**

#### **Data Source Name**

Artory is a blockchain-based platform that provides verifiable and transparent digital art provenance and ownership verification. Artory's API helps track the ownership history of art, ensuring that artists, buyers, and sellers have verifiable proof of ownership, and the transaction history is recorded immutably on the blockchain.

#### **API Endpoint URL**

`GET https://api.artory.com/v1/artworks/{artwork_id}/provenance`

#### **Purpose**

This schema validates the ownership and transaction history of a digital artwork, providing transparent provenance information. By using the Artory API, it enables users to verify whether an artwork is authentic, who its previous owners were, and if it was part of legitimate transactions, ensuring confidence in the purchase or sale of digital art.

#### **Sample JSON Response**

```json
`{
  "artwork_id": "xyz12345678",
  "title": "The Virtual Horizon",
  "artist": "Jane Doe",
  "current_owner": {
    "owner_id": "owner12345",
    "name": "John Smith",
    "ownership_start_date": "2024-12-01",
    "ownership_status": "active"
  },
  "ownership_history": [
    {
      "owner_id": "owner123",
      "name": "Alice White",
      "ownership_start_date": "2022-06-15",
      "ownership_end_date": "2024-11-30",
      "transaction_type": "sale",
      "transaction_amount": "2500 ETH",
      "transaction_date": "2024-06-01"
    },
    {
      "owner_id": "owner124",
      "name": "Bob Green",
      "ownership_start_date": "2021-02-10",
      "ownership_end_date": "2022-06-14",
      "transaction_type": "sale",
      "transaction_amount": "1800 ETH",
      "transaction_date": "2021-12-20"
    }
  ],
  "authenticity_status": "verified",
  "blockchain_proof": {
    "proof_type": "Ethereum Smart Contract",
    "contract_address": "0x123456789abcdef",
    "token_id": "1",
    "transaction_hash": "0xabcdef1234567890abcdef1234567890abcdef1234567890"
  },
  "expiration_date": "2025-12-31",
  "proof": {
    "type": "Blockchain Proof",
    "created": "2024-12-15T10:00:00Z",
    "verificationMethod": "did:artory:5678xyz",
    "proofPurpose": "assertionMethod",
    "jws": "eyJhbGciOiJFUzI1NiJ9..."
  }
}` 
```

#### **Technical Breakdown**

This schema ensures that an artwork's ownership and provenance are validated using blockchain technology, which provides transparent and immutable proof of its history. The Artory API is used to fetch the artwork's provenance details and verify its authenticity.

**Key Validation Conditions:**

-   **`authenticity_status`**: The artwork must have a status of `verified`, meaning its authenticity is confirmed by the blockchain.
-   **Ownership History**: Each transaction in the ownership history must be properly recorded, with details such as the transaction amount and dates.
-   **Blockchain Proof**: Each artwork must have blockchain-backed proof, including details like the smart contract address, token ID, and transaction hash.
-   **Expiration Date**: The artwork’s certification or provenance validity must not expire.
-   **Proof**: The response must contain cryptographic proof (e.g., JWS) ensuring that the provenance data has not been tampered with.

**Key Use Cases:**

-   Verifying the authenticity and ownership history of digital art for buyers and collectors.
-   Providing artists with a transparent and immutable way to track the ownership and transaction history of their artworks.
-   Ensuring that digital art transactions are legitimate, reducing the risk of counterfeiting or fraudulent sales.
-   Enabling auction houses, galleries, and marketplaces to confidently list verified digital artworks.

----------

### **Schema Code**

```json

`{
  "issuer": "Artory",
  "desc": "Verifies the ownership and provenance of digital artwork through blockchain-based verification.",
  "website": "https://artory.com",
  "APIs": [
    {
      "host": "artory.com",
      "intercept": {
        "url": "/v1/artworks/{artwork_id}/provenance",
        "method": "GET"
      },
      "assert": [
        {
          "key": "authenticity_status",
          "value": "verified",
          "operation": "="
        },
        {
          "key": "ownership_history[*].transaction_amount",
          "operation": "exists"
        },
        {
          "key": "ownership_history[*].transaction_type",
          "operation": "exists"
        },
        {
          "key": "blockchain_proof.contract_address",
          "operation": "exists"
        },
        {
          "key": "blockchain_proof.token_id",
          "operation": "exists"
        },
        {
          "key": "expiration_date",
          "value": "2025-12-31",
          "operation": ">"
        },
        {
          "key": "proof.jws",
          "operation": "exists"
        }
      ],
      "nullifier": "artwork_id"
    }
  ],
  "HRCondition": [
    "The artwork must have a verified authenticity status.",
    "All ownership transactions must be properly recorded with transaction amounts and dates.",
    "The blockchain proof must exist with proper smart contract address and token ID."
  ],
  "tips": {
    "message": "Ensure that the artwork's authenticity is confirmed and its blockchain transaction history is available."
  },
  "category": "Digital Art Ownership",
  "id": "0xartoryProvenanceValidation01"
}` 
```

----------

### **Demo/Test Case**

#### **Scenario**: A collector is purchasing a digital artwork and wants to verify its authenticity and ownership history before buying.

-   **Step 1**: The collector queries the Artory API using the `GET /v1/artworks/{artwork_id}/provenance` endpoint, providing the artwork’s unique `artwork_id`.
-   **Step 2**: The API returns a response confirming the artwork’s authenticity and providing details about its previous ownership, including the transaction amounts and dates.
-   **Step 3**: The collector checks if the blockchain proof exists, ensuring that the artwork's authenticity is backed by an immutable blockchain transaction.
-   **Step 4**: The collector verifies that the artwork’s ownership history matches their expectations (e.g., it has not been sold multiple times under false claims).
-   **Step 5**: If the artwork meets the authenticity and provenance criteria, the collector proceeds with the purchase. If there are any inconsistencies, the collector rejects the artwork or asks for further clarification.

----------

### **Real-world Use Case**

This schema can be integrated into online art marketplaces like OpenSea, SuperRare, or foundation.app, where digital artists sell their works as NFTs (Non-Fungible Tokens). Buyers and sellers can use this schema to verify that the artworks they’re purchasing or selling have legitimate provenance.

For example, a collector on OpenSea could use this schema to ensure that an artwork they wish to buy is verified as authentic and has a clean transaction history. Similarly, an artist could use this schema to prove to potential buyers that their digital artwork is authentic and has been sold to a verifiable owner previously.

This model provides a transparent, secure, and verifiable method of tracking digital art ownership, making it an essential tool for the growing NFT and digital art market.

----------

This schema focuses on providing provenance and authenticity verification for digital art through blockchain, ensuring buyers, sellers, and collectors can trust the transaction history and legitimacy of digital artworks. By integrating blockchain-based proof and ownership history, it offers a secure way to prevent fraud and guarantee the value and provenance of digital art.