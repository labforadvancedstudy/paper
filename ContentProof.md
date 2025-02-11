# Blockchain-Based Off-Chain Block Creation and NFT Issuance Algorithm for Digital Content Proof

## Authors: Jihyuk Im(zhugehyuk@gmail.com)

## Editors: ChatGPT o1-pro

## 1. Introduction

In today’s digital environment, various forms of content—images, videos, audio, etc.—are produced and distributed. However, proving the **creation time** and **originality** of such content remains a challenging issue, and it is not easy to guarantee that no tampering has occurred, even if digital signatures are included.

Consequently, methods that utilize **blockchain** to record the **creation time**, **creation device**, and **creation wallet (account)** of digital content, and then issue it in the form of an **NFT (Non-Fungible Token)** to enable **independent third-party verification**, have attracted attention. This paper proposes an algorithm for guaranteeing the authenticity and creation history of digital content by using a **blockchain-based off-chain block** structure and **multi-signature**.

Our proposed method aims to satisfy the following requirements:
1. **Reliability**: By linking the device information, wallet information, app integrity, and timestamp at the moment of content creation to the blockchain, it becomes impossible to tamper with this information afterward.
2. **Legal Evidence Applicability**: Based on digital signatures and PKI (Public Key Infrastructure), the signatures should be verifiable so that the timestamp recorded on the blockchain can be used as legal evidence.
3. **Scalability**: When numerous posts are generated in an actual service, **off-chain blocks** are created to minimize on-chain (main chain) transaction fees, and the hash of these blocks is periodically anchored on-chain.

In the following, we detail the overall system structure, key management, signature scheme, and the mathematical verification process. Building upon this, we then present how to design the metadata for the NFTs issued. Finally, we provide additional considerations and references that need to be addressed when implementing this approach.

---

## 2. Proposed System Architecture

### 2.1 Key Management

1. **DevicePriv, DevicePub**  
   - Private key and public key pair generated upon the first execution of the application (client).  
   - The public key (DevicePub) is registered on the server for device identification.  
   - The private key (DevicePriv) is stored in a secure storage (e.g., Secure Enclave, TrustZone) to protect it against rooting or jailbreaking.  
   - There is a risk of key exposure if the device is hacked or lost, so storing the key via hardware security modules (HSM) or establishing a key recovery policy should be considered.

2. **ProjectPriv, ProjectPub**  
   - Private/public key pair managed at the company (project) level.  
   - Used for signing blocks when creating off-chain blocks.  
   - If this key is exposed, the integrity of the entire blockchain could be compromised, so regular key replacement or HSM usage should be considered.

3. **WalletPriv, WalletPub**  
   - A private/public key pair for the user’s wallet.  
   - Used for issuing or possessing NFTs on the blockchain.  
   - An additional mapping for account information (e.g., user ID or mapping a blockchain address to an account) is managed separately.

### 2.2 Off-Chain Block Structure and Creation

In this design, **off-chain blocks** are created at fixed intervals (e.g., every 60 seconds). The post hashes that occur during that interval are included in the block, which is then signed with **ProjectPriv** to ensure integrity. Below is a simplified procedure:

1. **Block creation interval**: 60 seconds (or adjusted according to service needs).  
2. **Post aggregation interval**: Collect the post hashes created every 10 seconds, and include them in the off-chain block generated every 60 seconds.  
3. **Generating a new off-chain block**  
   ```
   new_block_signature = sign(ProjectPriv, {
       prev_block_hash,    // 512bit
       timestamp,          // block creation time
       list_of_posts_hash  // aggregated post hashes over 10-second intervals
   });
   new_block = {
       prev_block_hash,
       timestamp,
       list_of_posts_hash,
       signature_ProjectPriv = new_block_signature
   };
   new_block_hash = hash(
       prev_block_hash + timestamp + list_of_posts_hash + signature_ProjectPriv
   );
   ```
4. **On-chain Anchoring**  
   - The newly generated `new_block_hash` is periodically (e.g., every N minutes to 1 hour) recorded on-chain.  
   - By anchoring the block hash on-chain, it becomes possible to track whether the entire off-chain data has been tampered with.

### 2.3 Post Creation & Signature Flow

When a user creates a **post** (such as a photo, video, or audio) through the application, the following steps are performed:

1. **postDataHash**  
   - The hash of the original media (image, video, audio).  
   - May include the entire file or critical frames/metadata as needed.

2. **Watermark Insertion**  
   - The `postDataHash` or part of it is inserted as a watermark into the original media.  
   - The choice of watermarking technique should consider resistance to tampering and readability.  
   - Subsequently, `getWaterMark(postDataHash)` may reference the current off-chain block hash (the block generated so far).

3. **AppHash**  
   - A hash (512-bit, etc.) to verify the integrity of the application code.  
   - A hash of the app binary or a specific code snippet for a particular version.  
   - When the app is updated, each version’s hash should be managed separately to detect tampering.

4. **Signature Procedure**  
   - Device Signature
     ```
     device_signature = sign(DevicePriv, {
         postDataHash,
         current_block_hash,  // the current off-chain block hash
         AppHash
     });
     ```
     - Proves the post was created by the device (DevicePub) registered on the server.  
     - Prevents tampered or unauthorized client apps from signing.

   - Wallet Signature
     ```
     wallet_signature = sign(WalletPriv, {
         postDataHash,
         current_block_hash,
         AppHash,
         device_signature
     });
     ```
     - Proves that a specific wallet owner created the post.  
     - By mapping the wallet to an account, it can be tied to the user account requesting the post creation.

5. **Final Post Hash (postHash)**
   ```
   postHash = hash(
       postDataHash + current_block_hash + AppHash + 
       device_signature + wallet_signature
   );
   ```
   - During off-chain block creation, this is included in the `list_of_posts_hash` for chaining.

---

## 3. Mathematical Verification

This section summarizes how the above signature and hash structure can be mathematically verified.

### 3.1 Hash-Based Integrity Proof

- **Per-Post Integrity**  
  \[
  \text{postHash} = H\bigl(\text{postDataHash} \Vert \text{curr\_block\_hash} \Vert \text{AppHash} \Vert \text{device\_sig} \Vert \text{wallet\_sig}\bigr),
  \]  
  where \( H(\cdot) \) is a cryptographic hash function (e.g., SHA-256, SHA-512), and \(\Vert\) denotes secure concatenation.  
  - During re-verification, the same inputs concatenated and hashed must yield the same value to ensure integrity.

- **Per-Block Integrity**  
  \[
  \text{new\_block\_hash} = H\bigl(\text{prev\_block\_hash} \Vert \text{timestamp} \Vert \text{list\_of\_posts\_hash} \Vert \text{signature\_ProjectPriv}\bigr).
  \]
  - Includes \(\text{prev\_block\_hash}\) to form a chain of blocks.  
  - If any intermediate block is tampered with, all subsequent block hashes change, allowing integrity checks.

### 3.2 Signature Verification

- **Device Signature**  
  \[
  \text{device\_signature} = \text{Sign}\bigl(\text{DevicePriv},\, \text{msg}\bigr),
  \]  
  where \(\text{msg} = \text{postDataHash} \Vert \text{curr\_block\_hash} \Vert \text{AppHash}\).  
  - Verification requires \(\text{Verify}(\text{DevicePub}, \text{msg}, \text{device\_signature})\) to be true.

- **Wallet Signature**  
  \[
  \text{wallet\_signature} = \text{Sign}\bigl(\text{WalletPriv},\, \text{msg'}\bigr),
  \]  
  where \(\text{msg'} = \text{postDataHash} \Vert \text{curr\_block\_hash} \Vert \text{AppHash} \Vert \text{device\_signature}\).  
  - Verification requires \(\text{Verify}(\text{WalletPub}, \text{msg'}, \text{wallet\_signature})\) to be true.

- **Project Signature**  
  \[
  \text{new\_block\_signature} = \text{Sign}\bigl(\text{ProjectPriv},\, \text{blockMsg}\bigr),
  \]  
  where \(\text{blockMsg} = \text{prev\_block\_hash} \Vert \text{timestamp} \Vert \text{list\_of\_posts\_hash}\).  
  - Verification requires \(\text{Verify}(\text{ProjectPub}, \text{blockMsg}, \text{new\_block\_signature})\) each time a block is created.

Using this signature and hash structure, **any tampering of posts and blocks can be mathematically detected**. Each of the signed messages is unique (time, hash value, signature targets differ), and **delimiters or structural encoding** (e.g., Protobuf, JSON with specific tags) should be clearly defined to prevent **ambiguity (attacks on concatenation)**.

---

## 4. NFT Metadata Composition

When posts created under this algorithm are later issued as NFTs, the **NFT metadata** should include the following key items:

1. **NFT ID**:  
   - For example, directly use `postHash` as the unique ID of the NFT or create a separate token ID associated with it.

2. **Creation Timestamp**:  
   - The timestamp of the company’s blockchain recorded in the off-chain block.  
   - Can use `new_block.timestamp`.

3. **Off-Chain Block Hash**:  
   - The hash (`new_block_hash`) of the off-chain block containing the post.  
   - This is referenced at the time of on-chain anchoring.

4. **Post Data Hash (postDataHash)**:  
   - The hash of the original media (before/after watermark insertion).  
   - Used to verify the integrity by comparing it with the original file during checks.

5. **Device Information**:  
   - `DevicePub` (the device’s public key)  
   - `device_signature` (the device signature)  
   - Potentially includes the application code hash (`AppHash`)

6. **Wallet Information**:  
   - `WalletPub` (the wallet’s public key)  
   - `wallet_signature` (the wallet signature)  
   - The linked account (wallet address or user identifier)

7. **Project Signature Data** (optional):  
   - `ProjectPub` and the block signature (`new_block_signature`)  
   - May store the entire block signature in the NFT metadata for additional proof

This metadata can be defined in JSON format according to an NFT standard (ERC-721, ERC-1155, etc.), and subsequently, **servers or on-chain smart contracts** can reference a metadata URI to perform verification.

---

## 5. Verification and Proof Process

1. **Refer to the NFT → Retrieve Off-Chain Block**  
   - Using the `off-chain block hash` recorded in the NFT, query the off-chain block DB (or a dedicated verification node) published by the company.  
   - Check the block’s timestamp, list of posts, project signature, etc.

2. **Signature Verification**  
   - **Device Signature Verification**: Reconstruct the message with `postDataHash`, `current_block_hash`, and `AppHash`, along with `DevicePub`, `device_signature` from the NFT, and perform \(\text{Verify}(\text{DevicePub}, \dots)\).  
   - **Wallet Signature Verification**: Perform the same process with `WalletPub`, `wallet_signature`.  
   - **Project Signature Verification**: Check `new_block_signature` signed with `ProjectPriv` using `ProjectPub` during block creation.

3. **Recalculate Hashes**  
   - Recalculate `postHash`: concatenate `postDataHash + current_block_hash + ... + wallet_signature` and hash it.  
   - Recalculate `new_block_hash`: using `prev_block_hash + timestamp + list_of_posts_hash + signature_ProjectPriv`.  
   - All values must match the originals for a "no tampering" judgment.

4. **Confirm Creation Time and Entity**  
   - The `timestamp` of the off-chain block is confirmed as the creation time.  
   - `DevicePub` identifies the device, and the combination of `WalletPub` + account mapping identifies the specific user.

5. **Issuance of a Certificate**  
   - Based on the above verification results, generate a digital certificate (including verification logs, hash values, and signature results) that can be used as legal evidence.  
   - In case of any disputes in the future, the same procedure can be used for re-verification.

---

## 6. Additional Considerations

1. **Key Exposure Response**  
   - If `DevicePriv` or `ProjectPriv` is leaked, the integrity of the entire chain might be compromised, so **periodic key replacement** policies, HSM integration, or multi-signature (multi-sig) structures should be considered.

2. **Watermarking Techniques**  
   - Simple image steganography or advanced deep watermarking can be used.  
   - Must balance **robustness** (resistance to image/video editing) and **visibility** (where the court can verify it as legal evidence).

3. **Replay Attack Prevention**  
   - Provide a unique nonce or identifier for each post.  
   - Ensure each signature includes a timestamp or block hash so that the same signature cannot be reused.

4. **Time Synchronization**  
   - The off-chain block creation time and the on-chain record time must be **accurately synchronized**, possibly using NTP servers or an official timestamp authority for UTC.

5. **Structured Message Encoding**  
   - If you simply concatenate hash or signature inputs, there is a risk of ambiguity attacks.  
   - Using a format with a clearly defined structure (JSON, Protocol Buffers, ASN.1, etc.) before signing and hashing is recommended.

6. **Scalability**  
   - If numerous posts are generated, off-chain blocks and on-chain anchoring may become excessively large.  
   - Consider using Merkle trees to efficiently aggregate many hashes, or adopting **layer-2 solutions**.

---

## 7. Conclusion

This paper proposed a **digital content proof algorithm** based on a blockchain-driven off-chain block. The proposed structure uses a multi-signature scheme—(1) device signature, (2) wallet signature, (3) project signature—to transparently confirm the content creation time and creator (device, wallet, account), while ensuring **integrity and immutability** by periodically anchoring off-chain block hashes on-chain.

NFTs issued subsequently include this information, and upon request, a server or an independent verifier can conduct **mathematical verification** (signature checks, hash recalculations) so that even in legal disputes, the creation time and authenticity of the content can be quickly verified. For real-world implementation, secure key management, selection of a watermarking method, replay attack prevention, time synchronization, and structural encoding must be thoroughly addressed.

---

## 8. References

1. **Merkle, R.** (1989). *A Certified Digital Signature*. In **Advances in Cryptology—CRYPTO '89** (pp. 218–238). Springer.  
   - A classic paper introducing fundamental theories on hash trees and digital signatures.

2. **Nakamoto, S.** (2008). *Bitcoin: A Peer-to-Peer Electronic Cash System*.  
   - The original concept of the distributed ledger system known as blockchain.

3. **Huh, S.-Y., Choi, S., & Kim, S.** (2017). *Managing IoT devices using blockchain platform*. In **2017 19th International Conference on Advanced Communication Technology (ICACT)** (pp. 464–467). IEEE.  
   - Presents methods for managing devices and ensuring trust via blockchain.

4. **Kesse, D.** (2019). *A blockchain-based approach for digital evidence management*. **Journal of Digital Forensics, Security and Law**, 14(2), 25–39.  
   - A case study on utilizing blockchain for the management and verification of digital evidence as legal proof.

5. **Zhu, H., & Badr, Y.** (2018). *Identity management systems for the Internet of Things: A survey towards blockchain solutions*. **Sensors**, 18(12), 4215.  
   - Discusses identity/key management and blockchain integration in IoT and distributed environments.

6. **ERC-721: Non-Fungible Token Standard**  
   - [https://eips.ethereum.org/EIPS/eip-721](https://eips.ethereum.org/EIPS/eip-721)  
   - The Ethereum standard proposal for NFTs.

---

## 9. Closing Remarks

The proposed structure in this paper combines off-chain blocks with on-chain anchoring to offer a relatively efficient way to utilize blockchain when a large number of posts are created. For real-world application, it is crucial to consider **app version management**, **secure key storage using HSM**, and **global time synchronization** to cover all security and system issues.

Through this approach, the resulting NFT becomes a digital asset verifiable by anyone on the blockchain, and upon server verification requests, it provides **mathematical and cryptographic proof** (of creation time, creation device, creation wallet, and account). Ultimately, it offers a new form of certification that enhances the reliability of digital content and can be used as legal evidence.

---

### (Additional If Needed)
- For genuine legal evidence usage, compliance with the electronic document acceptance requirements of the relevant courts (electronic signature laws, eIDAS regulations, etc.) should be considered from the outset of the project.  
- The specific parameters of the watermarking technique (insertion capacity, perceptual quality, etc.) depend on the media’s characteristics, requiring further study.  
- It is recommended to build a prototype, measure performance (block creation speed, signature/verification overhead, etc.), and establish optimization strategies.
