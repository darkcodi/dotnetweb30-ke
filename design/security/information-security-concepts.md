# Information security concepts

### CIA Triad

{% hint style="success" %}
The **CIA triad** of _confidentiality_, _integrity_, and _availability_ is at the heart of information security.
{% endhint %}

#### **Confidentiality**

**Confidentiality** is the property, that information is not made available or disclosed to unauthorized individuals, entities, or processes. Examples of confidentiality of electronic data being compromised include laptop theft, password theft, or sensitive emails being sent to the incorrect individuals.

While similar to "privacy," the two words aren't interchangeable:

| BASIS FOR COMPARISON | PRIVACY | CONFIDENTIALITY |
| :--- | :--- | :--- |
| Meaning | The state of being secluded is known as Privacy. | Confidentiality refers to the the situation when it is expected from someone that he will not divulge the information to any other person. |
| What is it? | It is the right to be let alone. | It is an agreement between the persons standing in fiduciary to maintain the secrecy of sensitive information and documents. |
| Concept | Limits the access of the public. | Prevents information and documents from unauthorized access. |
| Applies to | Individual | Information |
| Obligatory | No, it is the personal choice of an individual | Yes, when the information is professional and legal. |

#### **Integrity**

**Integrity** means maintaining and assuring the accuracy and completeness of data over its entire lifecycle. ****This means that data cannot be modified in an unauthorized or undetected manner.

#### **Availability**

**Availability** means the computing systems used to store and process the information, the security controls used to protect it, and the communication channels used to access it must be functioning correctly. High availability systems aim to remain available at all times, preventing service disruptions due to power outages, hardware failures, and system upgrades. Ensuring availability also involves preventing denial-of-service attacks, such as a flood of incoming messages to the target system, essentially forcing it to shut down.

## Authentication/Authorization concepts

| **Authentication** | **Authorization** |
| :--- | :--- |
| Determines whether users are who they claim to be | Determines what users can and cannot access |
| Challenges the user to validate credentials \(for example, through passwords, answers to security questions, or facial recognition\) | Verifies whether access is allowed through policies and rules |
| Usually done before authorization | Usually done after successful authentication |
| Generally, transmits info through an ID Token | Generally, transmits info through an Access Token |
| Generally governed by the OpenID Connect \(OIDC\) protocol | Generally governed by the OAuth 2.0 framework |
| Example: Employees in a company are required to authenticate through the network before accessing their company email | Example: After an employee successfully authenticates, the system determines what information the employees are allowed to access |

