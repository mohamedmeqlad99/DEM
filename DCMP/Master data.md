## master data
is data about business entities that provide context for business transactions 

it is a consistent and uniform set of identifiers and extended attributes that describe the core entities of the enterprise including customers , prospects , citizens , suppliers ,etc![[example of master data.png]]

## reference data
it is data that used to classify or categorize other data
like:
- postal code 
- country
- language 
- segments 
## master data management 
the process of creating and maintaining a single master record or single source of truth for each entity in business 

through MDM organizations get a trusted current view of key data that can be shared across the business and used for reporting and better decision making

MDM
- improve data quality 
- improve decision making 
- reduce time to market 
- reduce workload 
### 1. **Registry Style**

- **Overview**: The registry style centralizes metadata about master data without physically storing the actual data in one place. Instead, it creates a "registry" that references data from multiple source systems.
- **How It Works**:
    - Source systems retain the master data.
    - A central registry indexes the master data using unique identifiers (e.g., IDs).
    - Queries are routed to the registry, which fetches the needed data from source systems.
- **Advantages**:
    - Minimal disruption to existing systems.
    - No need to replicate data, reducing storage requirements.
    - Easier to implement than other styles.
- **Challenges**:
    - Performance may depend on the latency of source systems.
    - Real-time consistency may be challenging if source systems aren't synchronized.

---

### 2. **Consolidation Style**

- **Overview**: In this style, the master data is copied from source systems into a central repository but remains unchanged in the source systems.
- **How It Works**:
    - Source systems maintain their data.
    - The central MDM repository consolidates and harmonizes data for reporting and analytics purposes.
    - Data in the central repository is used as a "golden copy" for specific use cases but does not feed back to source systems.
- **Advantages**:
    - Provides a unified view for analysis and reporting.
    - Easier integration with data warehouses and analytics tools.
- **Challenges**:
    - Data remains inconsistent across source systems.
    - Not ideal for operational use or real-time applications.

---

### 3. **Coexistence Style**

- **Overview**: This approach combines the registry and consolidation styles. A central repository stores a "golden record," which is updated and synchronized with source systems as needed.
- **How It Works**:
    - Source systems and the central MDM repository exchange updates bi-directionally.
    - Master data can be maintained in either the MDM repository or the source systems.
- **Advantages**:
    - Offers flexibility for both operational and analytical use cases.
    - Enables a single source of truth while allowing updates in source systems.
- **Challenges**:
    - Requires robust synchronization mechanisms.
    - Implementation can be complex and costly.

---

### 4. **Transaction Style**

- **Overview**: The MDM repository becomes the system of record (SOR), and all updates to master data happen in the central MDM system.
- **How It Works**:
    - Source systems reference the master data from the MDM system.
    - Changes are made directly in the MDM repository and propagated to source systems as needed.
- **Advantages**:
    - Ensures a single, consistent version of the truth across the organization.
    - Simplifies governance and compliance.
- **Challenges**:
    - Requires significant changes to existing systems and workflows.
    - Higher implementation complexity and cost.

---

### 5. **Hybrid Style**

- **Overview**: Combines elements of the other styles to address specific organizational needs.
- **How It Works**:
    - For example, a hybrid implementation might use the coexistence style for operational data and the consolidation style for analytics.
- **Advantages**:
    - Highly customizable to meet unique requirements.
- **Challenges**:
    - Complex design and governance are needed to ensure smooth operations.

---

### Key Considerations for Choosing an MDM Style

- **Business Needs**: Operational consistency vs. analytical insights.
- **Existing Infrastructure**: Compatibility with current systems and processes.
- **Budget**: Cost of implementation and maintenance.
- **Data Volume and Complexity**: How much data needs to be managed and its complexity.
- **Governance Requirements**: Regulatory compliance and data quality standards.

Each MDM style serves different use cases, and organizations often start with one style and evolve toward more sophisticated approaches as their needs grow.