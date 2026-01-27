# Azure Verified Modules (AVM)

Azure Verified Modules (AVM) zijn een door Microsoft geïnitieerde en onderhouden set van gestandaardiseerde IaC-modules voor Azure, beschikbaar voor Bicep en Terraform.
Een AVM wordt onderhouden door een medewerker van Microsoft (de *module owner*).
Wanneer deze medewerker van rol veranderd wordt de AVM overgedragen naar een nieuwe eigenaar om continuïteit te borgen.

AVMs bestaan uit modules die volgens Microsoft’s _Well-Architected Framework (WAF)_ zijn ontworpen, getest en gedocumenteerd, en bevatten zowel Resource Modules als Pattern Modules:

| Module Type | Beschrijving |
| --- | --- |
| Resource Modules | Deployen één Azure resource met ingebouwde best practices (security, RBAC, netwerken, enz.). |
| Pattern Modules | Combineren meerdere resource modules tot veelgebruikte architecturen of patronen. |
| Utility Modules | (Draft)	Reusable functions/routines zonder echte resource deploys (in draft-fase). |

## Kernprincipes van AVM

* **Secure and available by default**  
  - Standaard secure configuraties  
  - Best practices automatisch toegepast  
  - Bijvoorbeeld: zone-redundancy standaard aan, private endpoints i.p.v. public exposure, secure defaults voor identity & access
 
* **Enterprise-grade standaarden**  
  - Alignement met Microsoft Well-Architected Framework  
  - Ingebouwde support voor:
    - Identity & RBAC
    - Logging & monitoring
    - Networking patterns
    - Compliance & governance structuren

* **Lifecycle & onderhoud**
  - Versiebeheer via officiële module registry  
  - Actief onderhouden door Microsoft + community  
  - Updates bij nieuwe Azure features  
  - Backwards compatibility waar mogelijk
 
## Architectuurfilosofie

AVM is ontworpen als **standaard bouwblok-architectuur**:

- Kleine, herbruikbare modules
- Compositie via pattern modules
- Scheiding tussen:
  - infrastructuurlogica
  - architectuurpatronen
  - omgevingsspecifieke configuratie (OTAP)
 
## Vergelijking met custom Bicep modules

**Custom Bicep Modules**
- Maximale flexibiliteit
- Volledige controle over architectuur
- Eigen verantwoordelijkheid voor security, updates en best practices
- Sneller maatwerk, maar meer onderhoud

**AVM**
- Standaardisatie
- Best practices by default
- Minder onderhoud
- Minder vrijheid in afwijkende architectuurkeuzes
- Meer configuratie i.p.v. code

**Hybride model (aanbevolen):**
- AVM voor:
  - generieke resources (Storage, Key Vault, VNET, Log Analytics, etc.)
  - baseline infrastructuur
  - security-sensitive componenten
- Custom modules voor:
  - OTAP-specifieke orchestration
  - project-specifieke architectuur
  - domeinspecifieke patronen
  - integratie-logica

## Linkjes

* [Bicep Registry Modules (repository)](https://github.com/Azure/bicep-registry-modules/)
* [Azure Verified Modules (documentatie)](https://aka.ms/AVM/)
* [Azure Verified Modules (support)](https://aka.ms/AVM/support/)
