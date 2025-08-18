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







<!-- --- Authentication generates a token for access for a ttl, once token is issued it is used for authentication until it is expired, permissions or the scope of token is also associated with the token -->
