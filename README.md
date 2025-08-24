# Hashicorp Vault

**What is Vault?**
> [!NOTE]
> Vault provides centralized, well-audited privileged access and secret management for mission-critical data whether you deploy systems on-premises, in the cloud, or in a hybrid environment.

- Manages secrets and protect sensitive data
- Provides a single source of secrets for both humans and machines
- Provides complete life-cycle management
- Eliminate secret sprawl, Securely store secrets
- Provide governance for access to secrets

**How Vault Works?**
- Vault has 3 interfaces: GUI, CLI, API
- Authentication mechanism
- Token for authenticated user

**Why choose Vault?**
- Every cloud platform has its own secret management tool or mechanisms
- Vault can be integrated with all of them making cloud migration easy 
- Learning curve is reduced for different cloud secret management and access management mechanisms
- Multi-cloud infrastructure is made easier

**Benefits of Vault**
- Long lived static secrets
- Dynamically generate secrets
- Fully featured API
- Identity based access across cloud platforms
- Provide encryption as a service
- Act as a root or intermediate certificate authority

**Vault use cases**
- Central secret store
- Migrate to dynamic secrets
- Store data with centralized encryption systems
- Automate cert generations
- IAM and IAM based access: Quick scale, better timing

> [!NOTE]
> **Static VS Dynamic secrets**
>
> | Static | Dynamic |
> | -------| ------- |
> | Valid for eternity | Short lived |
> | Manual password rotation | Automatic revocation |
> | Frequently shared accross the team | Each system can retrieve unique secrets |
> | Reused accross systems | Programatically accessed |
> | Susceptible to password push to repo | No human interaction |
> | Privileged | Follow principle of least privileged |


## Vault Architecture
### Vault Components
- **Storage Backends**
    - Configures location for storage of vault data
    - Defined in main vault configuration file
    - Data is encrypted in transit (TLS) and at rest using AES256
    - Some storages are for high availability and others for better management and data protection
    - Only one storage backend per vault cluster

- **Secrets Engines**
    - Manages secrets
    - Secret engines can store, generate and encrypt data
    - Many engines can connect to other services to generate dynamic credentials on demand
    - There can be multiple instances of same type of secret engine
    - Secret engines are mounted at path and all interactions are done with the path itself

- **Authentication methods**
    - Manages authentication and manages identities
    - Responsible for assigning identity and policies to users
    - Multiple authentication methods can be enabled 
    - There are 2 types of authentication methods classes: human and machine
    - Once authenticated, vault issues a token to the client or user to make all subsequent vault requests until TTL
    - Each token has a policy and a TTL
    - Default authentication method for vault is also token based

- **Audit devices**
    - Keeps detailed log for all requests and responses to vault
    - Audit log is formatted using json
    - Sensitive info is hashed before logging
    - There can be multiple audit devices enabled
    - Vault required at least one audit device to write the log before completing the vault request - if enabled
    - Prefers safety over availability

### The Encryption Barrier
- The diagram can be seen at [Vault Docs](https://developer.hashicorp.com/vault/docs/about-vault/how-vault-works#the-encryption-barrier)

- **Vault Paths**
    - Everything in vault is path based
    - The path prefix tells vault which component a request should be routed
    - Secret engines, authentication methods and audit devices are mounted at paths
    - Paths available are dependent on features that are enabled in the vault
    - System backend is the default backend in vault which is mounted at `/sys` endpoint
    - Every vault component has its own default path

### Vault Data Protection
Master key protects encryption key\
Encryption key protects vault data\
Encryption key is stored in vault node memory

- **Master Key**
    - Used to encrypt and decrypt encryption key
    - Created using initialization and re key operations
    - Never written to storage when using traditional unseal mechanism
    - Written to core/master (storage backend) when using `auto unseal`

- **Encryption Key**
    - Used to encrypt and decrypt the vault data written to storage backend
    - Encrypted by the master key
    - Stored alongside the data in a keyring on the storage backend
    - Can be easily rotated

### Seal and Unseal
- Vault starts in sealed state, meaning it knows where to access the data but can not decrypt it. Users can seal it manually as well
- Almost no operations are possible when the vault is in sealed state (only status check and unsealing are possible)
- Unsealing vault means that a node can reconstruct the master key in order to decrypt the encryption key, and ultimately read the data
- After unsealing, the encryption key is stored in memory
- Every node in the cluster should be unsealed to do any operations

- Sealing vault means it throws away the encryption key and requires another unseal to perform any further operations

> [!NOTE]
> **When to seal vault?**
> - Key shards are exposed
> - Detection of a breach or compromise of network
> - Spyware/malware on the vault nodes

**Seal and Unseal Options**
- **Key Sharding (Sharmir algorithm)**
    - The master key is broken into N parts and given to N people
    - While unsealing the vault,it requires a threshold of keys, threshold can be set at vault initialization
    - It is the default option
    - No single person should have access to all those shards
    - Shards should not be stored online
> [!NOTE]
> We can have PGP keys of people before initialization of vault so that even if keys given by vault, the keys are only readable by respective person only. This increases the security of the key. The minimum number of keys required is equal to number of threshold
- Cloud Auto Unseal (cloud key management like KMS)
- Transit Auto Unseal















<!-- commands: `vault status` -->

<!-- --- Authentication generates a token for access for a ttl, once token is issued it is used for authentication until it is expired, permissions or the scope of token is also associated with the token -->
