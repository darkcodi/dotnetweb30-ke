# Access Control Models

### Mandatory Access Control \(MAC\)

MAC is a static access control method. Resources are classified using labels. Clearance labels are assigned to users who need to work with resources. For example, some data may have “top secret” or level 1 label. Other information may have a “secret” or level 2 level. Other information may have “free” or level 3 level. So, data can only be accessed by people with certain clearance level.

With MAC method the data owner can’t decide which individuals have access to the data. The data owner can only decide what level of clearance is required to see the data and who has which level of clearance. So, this model is not based on identity, it is based on policy or matching of labels.

### Discretionary Access Control \(DAC\)

When using DAC method, the owner decides who has access to the resource. So decisions are made directly for subjects. To accomplish this we use Access Control Lists \(ACL\). ACL controls who has access to the resource and the data owner sets the rights or permissions.

### Role Based Access Control \(RBAC\)

When using role-based access control method data access is determined by the role within the organization. It is not determined for individual users. This is a hybrid between MAC and DAC. The role can be a job position, group membership, or security access level. Users are members of some role and that gives them access to certain resources in the organization.

### Other models

* Attribute-based Access Control \(ABAC\)
* History-Based Access Control \(HBAC\)
* Identity-Based Access Control \(IBAC\)
* Organization-Based Access control \(OrBAC\)
* Rule-Based Access Control \(RAC\)

