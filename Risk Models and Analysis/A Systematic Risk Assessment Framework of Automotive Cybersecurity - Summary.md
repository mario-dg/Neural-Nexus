https://doi.org/10.1007/s42154-021-00140-6
Yunpeng Wang, Yinghui Wang, Hongmao Qin, Haojie Ji, Yanan Zhang, Jian Wang
## Framework Description
![[Framework.png]]
#### 1. Risk Identification:
- **TOE/Use Case Analysis:** Target of Evaluation (TOE) or use cases must be thoroughly analyzed to understand what needs to be protected.
- **Asset Identification:** This involves identifying all the assets that could be affected by cybersecurity threats.
- **Asset Category:** Assets are categorized to manage them efficiently and apply appropriate security measures.
- **Data Flow Diagram:** Creating a visual representation of the data flow to identify where data moves and can be potentially compromised.
- **Threat Identification using STRIDE Model:** STRIDE is a model used to identify security threats by focusing on Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege.
- **Threat Scenario:** Developing scenarios in which these threats could be realized helps in understanding the potential impact and required defenses.
#### 2. Risk Analysis:
- **Impact Assessment:** This includes evaluating the impact of a threat materialization on safety, financial aspects, operations, privacy, and legislation.
- **Attack Analysis:**
	- **Attack Path Analysis:** Identifying possible paths an attacker could take.
	- **Attack Tree:** A branching diagram showing the possible routes an attack could take.
	- **Attack Feasibility Assessment:** Determining how likely an attack is to occur.
	- **Attack Potential:** Assessing the potential of an attacker successfully exploiting a vulnerability.
	- **Attack Vector:** The path or means by which an attacker can gain access to a computer or network server in order to deliver a payload or malicious outcome.
	- **CVSS Exploitability:** Referring to the Common Vulnerability Scoring System to gauge the ease and impact of an attack.
#### 3. Risk Assessment:
- **Risk Value:** The quantification of risk, possibly using an empirical equation.
- **Risk Matrix:** A matrix used to define the level of risk by considering the consequence and likelihood of a potential event.
- **Global Rating Algorithm:** An algorithm that takes various factors into account to provide a global risk rating.
- **Risk Level:** The final determination of risk level, which could be low, medium, or high based on the aggregated data.

## General Paper Summary
The paper presents a systematic risk assessment framework for automotive cybersecurity, emphasizing the need for comprehensive analysis throughout the vehicle's lifecycle due to evolving cyber threats. Key components include:

- **Introduction to Automotive Cybersecurity Challenges**: Recognizes the complexity and connectivity of modern vehicles, increasing vulnerability to cyber-attacks, and the importance of cybersecurity risk assessments.
- **Survey on Existing Risk Assessment Methods**: Discusses methods like STRIDE, CVSS, OWASP, and their application in automotive security, highlighting the gaps in current approaches.
- **Systematic Risk Assessment Framework**: Proposes a new framework consisting of risk identification, analysis, and assessment phases, leveraging STRIDE and attack trees for detailed threat evaluation and introducing a novel automotive cybersecurity risk matrix for quantifying risks.
- **Application of the Framework**: Demonstrates the framework's effectiveness through a case study on a Telematics Box (T-Box), showcasing how the proposed method systematically addresses cybersecurity threats.
- **Conclusion**: Affirms the framework's utility in identifying, analyzing, and assessing cybersecurity risks across the vehicle lifecycle, providing a foundation for future research and enhancement of automotive cybersecurity measures.

This framework incorporates specific processes and methods to effectively analyze potential attack paths, integrating changes in threat environments and available information, thereby offering a comprehensive approach to automotive cybersecurity risk assessment.

## Shortcomings of Existing Risk Assessment Frameworks as mentioned in the Paper
Based on the survey of existing risk assessment methods within the paper, the methods are grouped according to the specific methodologies they use, such as STRIDE, CVSS, OWASP, EVITA, and a combination of EVITA with other methods. Here's a detailed summary of the mentioned papers, categorized by the risk assessment methods used, along with their shortcomings and gaps:

#### STRIDE Methodhttps://doi.org/10.1007/s42154-021-00140-6
- Focus shifts from identifying specific attacks to the outcomes of potential attacks, requiring less cybersecurity expertise. However, it lacks depth in threat analysis and does not cover all aspects of attack possibility or impact parameters.
- In automotive applications, the STRIDE model was integrated with hazard analysis and risk assessment, considering cyberattack goals related to safety use cases. However, it only considered knowledge, tools, and threat criticality, omitting other attack possibilities or impact parameters.
#### CVSS (Common Vulnerability Scoring System)
- While CVSS is directly applicable to rating IT security vulnerabilities, only some indicators can be adapted for automotive cybersecurity risk elements, indicating a need for customization in automotive contexts.
#### OWASP (Open Web Application Security Project)
- Mainly focuses on web application security, potentially leading to inconsistencies due to its extensive parameters when applied to automotive cybersecurity risk assessments.
#### EVITA Method
- Provides a detailed definition of safety parameters but vague definitions for financial, operational, and privacy impacts. It did not consider the legislative factor in risk rating and focused on potential attacks without addressing the dynamic and practical nature of these threats.
#### Combined EVITA and Other Methods
- **Boudguiga et al.** proposed combining EVITA with TVRA (Threat Vulnerability and Risk Analysis) methods, improving the attack tree method with functional descriptions. However, the feasibility of this risk analysis method for cooperative engines was not demonstrated.
- **Dominic et al.** combined STRIDE classification with reference architecture for automated driving, increasing the evaluation workload due to complex threat model parameters.
- **Monteuuis et al.** considered human omissions and trustworthiness in autonomous vehicles using an improved STRIDE model and attack tree method, presenting a novel idea but adding to the complexity.
#### Overall Gaps Across Methods
- Many methods focus on the concept phase of the vehicle lifecycle, lacking depth in addressing the full spectrum of automotive cybersecurity challenges.
- Existing methods do not fully account for the changes in the threat environment, evaluation target (TOE), and available information throughout the vehicle lifecycle, leading to potential gaps in comprehensive risk assessment.
- The attack tree method, although used in various assessments, requires highly specialized evaluators, and when combined with STRIDE, may lack the necessary depth and detail for thorough threat analysis.

This survey illustrates that while numerous methodologies offer frameworks for assessing automotive cybersecurity risks, they often lack comprehensiveness, adaptability to the automotive context, or the ability to address the entire vehicle lifecycle. These gaps highlight the need for more holistic and adaptable frameworks, such as the one proposed in the paper, which aims to cover these deficiencies.

## Example Usage of the Proposed Framework
Chapter 4 of the paper, "Risk Assessment Application," details a practical application of the proposed systematic risk assessment framework through a case study on a Telematics Box (T-Box), a critical component of automotive network connections. Here's a comprehensive summary focusing on the assessment process:

#### Telematics Box (T-Box) Overview 
  - It's a key device in automotive network systems, integrating various communication modules (MCU/CPU, GPS, 3G/4G, Wi-Fi, Bluetooth) to connect vehicle networks with external networks via cloud platforms.
  - T-Box supports functionalities like vehicle remote control, anti-theft systems, firmware updates over-the-air, etc.
  - The system's complexity and multiple communication interfaces expose it to potential cybersecurity threats.
#### Cybersecurity Risk Assessment of T-Box
  - The assessment begins with a data flow analysis to understand how commands, like door-unlocking instructions, are processed from the user's mobile app through the TSP cloud platform to the T-Box and eventually to the vehicle's controller area network (CAN).
  - Attack Scenario: Attackers could reverse-engineer the T-Box firmware to send spoofed control commands, exploiting vulnerabilities in the in-vehicle infotainment system (IVI) accessed through a hotspot, leading to unauthorized command execution.
#### Attack Feasibility Assessment
  - Utilizes attack potential-based feasibility parameters, considering the attacker's cybersecurity knowledge, required knowledge about the target of evaluation (TOE), necessary equipment, and the attack's window of opportunity.
  - Assessment Results: The attack scenario was deemed feasible, with moderate attack feasibility level (AL = 2) based on the evaluation of expertise, knowledge, window of opportunity, and equipment required for the attack.
#### Impact Assessment
  - Evaluates the potential impacts of an attack on safety (S), finance (F), operation (O), and privacy or legislation (P).
  - The assessed scenario showed financial loss (due to potential theft) and operational impacts, with no direct impact on safety or privacy. The impact level (IL) was set to 2.
#### Risk Level Determination
  - Using the proposed cybersecurity risk matrix, the risk level value was determined based on the impact level and attack feasibility level, resulting in a risk level value of 2.
  - This level of risk suggests that the assessed scenario poses a moderate risk, requiring appropriate security measures to mitigate.
#### Conclusion of the Case Study
  - The case study validates the applicability and effectiveness of the proposed risk assessment framework, demonstrating its utility in identifying and assessing cybersecurity risks in automotive systems like the T-Box.
  - The results provide valuable insights for developing targeted security measures to protect automotive systems against identified risks.

This application showcases the framework's comprehensive approach, combining detailed threat scenario analysis, impact assessment, and feasibility evaluation to quantify cybersecurity risks systematically. It highlights the framework's potential to enhance automotive cybersecurity by facilitating informed decision-making regarding risk mitigation strategies.