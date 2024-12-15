
### **Schema Proposal: Secure Digital Identity Verification for Remote Work (Using LinkedIn and DID (Decentralized Identifiers))**

#### **Data Source Name**

LinkedIn and Decentralized Identifiers (DID). LinkedIn is a widely used professional networking platform, while DID is a decentralized and self-sovereign identity standard that allows individuals to own and control their identity without relying on centralized authorities. DIDs are often associated with blockchain networks for security and privacy.

#### **API Endpoint URL**

-   **LinkedIn Profile Data (Public)**: `GET https://api.linkedin.com/v2/me`
-   **DID Document Resolution**: `GET https://{DID_PROVIDER_URL}/{did}`

#### **Purpose**

This schema validates an individual's professional identity for secure remote work by combining traditional online professional profiles (e.g., LinkedIn) with the security and privacy features of decentralized identifiers (DID). The goal is to ensure that remote workers' identities are verified while respecting privacy and offering a high level of trust for both employers and employees.

#### **Sample JSON Response (LinkedIn and DID Integration)**

```json
`{
  "employee_id": "1234567890",
  "first_name": "Jane",
  "last_name": "Doe",
  "linkedin_profile": "https://www.linkedin.com/in/janedoe",
  "did_document": "did:example:1234567890abcdefghi",
  "verified_on_linkedin": true,
  "verified_on_did": true,
  "did_key": "did:example:1234567890abcdefghi",
  "professional_title": "Software Engineer",
  "employer": "Tech Solutions Inc.",
  "remote_work_verified": true,
  "contract_valid": true,
  "contract_expiry_date": "2025-12-31"
}` 
```

#### **Technical Breakdown**

This schema combines LinkedIn profile validation and DID verification to prove the identity of remote workers.

-   **LinkedIn Profile Verification**: The `linkedin_profile` field is validated to ensure that the person has an active LinkedIn profile and the profile data matches the provided information. The `verified_on_linkedin` field confirms whether the individual is authenticated.
    
-   **DID Verification**: The `did_document` field points to a DID document that contains identity-related information on the blockchain. The DID document can be verified through decentralized networks for enhanced privacy and trust. The `verified_on_did` field confirms that the DID document exists and is valid, linking the individual’s DID to their LinkedIn profile for trust.
    
-   **Remote Work and Contract Validation**: The `remote_work_verified` field confirms whether the individual has been verified as eligible for remote work based on their contract. The `contract_valid` and `contract_expiry_date` fields ensure that the worker has a valid contract with their employer.
    

#### **Key Use Cases**

-   **Secure Remote Worker Verification**: Employers can use this schema to validate the identity of remote workers while ensuring that they are authenticated on both a professional network (LinkedIn) and through a decentralized self-sovereign identity system (DID).
-   **Contract and Employer Verification**: This schema allows the validation of an individual’s work contract status and employer relationship, ensuring that remote workers are currently employed and their contracts are valid.
-   **Anti-Fraud Measures in Hiring**: The schema helps to prevent identity fraud and provides a secure method for verifying identities, which is essential in the hiring process, especially in remote work environments.

#### **Schema Code**

```json
`{
  "issuer": "LinkedIn & DID",
  "desc": "Verifies the identity and employment status of a remote worker through LinkedIn and Decentralized Identifiers.",
  "website": "https://www.linkedin.com",
  "APIs": [
    {
      "host": "api.linkedin.com",
      "intercept": {
        "url": "/v2/me",
        "method": "GET"
      },
      "assert": [
        {
          "key": "linkedin_profile",
          "operation": "exists"
        },
        {
          "key": "verified_on_linkedin",
          "value": "true",
          "operation": "="
        }
      ]
    },
    {
      "host": "{DID_PROVIDER_URL}",
      "intercept": {
        "url": "/{did}",
        "method": "GET"
      },
      "assert": [
        {
          "key": "did_document",
          "operation": "exists"
        },
        {
          "key": "verified_on_did",
          "value": "true",
          "operation": "="
        }
      ]
    }
  ],
  "HRCondition": [
    "The worker must have an active LinkedIn profile and a valid DID document to confirm their professional identity and employment status."
  ],
  "tips": {
    "message": "Ensure your LinkedIn profile is up-to-date and that your DID is properly associated with your professional identity for secure verification."
  },
  "category": "Remote Work Identity Verification",
  "id": "0xLinkedinDIDVerificationSchema01"
}` 
```

#### **Demo/Test Case**

-   **Scenario**: An employer wants to verify the identity and contract status of a potential remote software engineer.
    1.  The potential employee provides their LinkedIn profile URL and DID.
    2.  The employer queries the LinkedIn API to confirm the validity of the LinkedIn profile and check if the profile is verified.
    3.  The employer then queries the DID provider to validate the decentralized identity of the employee and check if the DID document is valid.
    4.  The schema validates both LinkedIn and DID information, ensuring that the employee is indeed who they claim to be.
    5.  The schema also confirms the employee's eligibility for remote work by checking the validity of their contract and employer association.

#### **Real-World Use Case**

This schema can be implemented by remote work platforms or HR software systems to securely verify the identities of remote employees. It allows employers to confirm both the professional identity and contract status of remote workers, ensuring that only verified individuals are allowed to join their team. Additionally, it leverages decentralized technology (DID) to enhance privacy and security, which is essential for sensitive remote work scenarios where data protection is paramount.