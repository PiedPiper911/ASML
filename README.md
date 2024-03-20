# ASML
This is a document that introduces the design of ASML language, including its design objectives, lexical rules, and grammar rules.

## Preface

Based on the application scenario modelling approach, combined with the UAV swarm mission description languages SML, SML-E and GML studied in the previous research, this document designs an Application Scenario Modeling Language (ASML) for UAV swarms on the basis of which to describe the scenario models constructed by the application scenario modelling approach and reasonably characterize the scenario tasks, resources and constraint information to achieve accurate and efficient description of the applications of UAS under different scenarios. The ASML is designed to describe the scenario models constructed by the application scenario modelling approach, and to reasonably characterize the tasks, resources and constraints of the scenarios, so as to accurately and efficiently describe the applications of the UAV systems in different scenarios. In this document, the lexical and syntactic rules are determined and an extensible markup language-based approach is adopted to design an application scenario modelling language with good readability, extensibility and reusability.

## Design Goal

The design needs to be guided by the principle of achieving basic linguistic competence while reflecting the precision and specialization of the UAV swarm oriented domain. In designing ASML, this language refers to the design methodologies of other cluster task description languages such as SML, SML-E and GML.

- Needs to adapt to complex and diverse UAV swarm application scenarios, so it also needs to provide good scalability and reusability.

- Separating scenario descriptions from underlying system implementations lowers the threshold to enable rapid user interaction with a swarm of drones.

  

## Lexical Rule

In order to more accurately describe the scene model constructed by the application scene modelling approach, reasonable lexical rules are needed to carry out clear and explicit definition of the lexical rules of the elements in the application scene modelling language. These include constituent elements, data types and keywords. Firstly, the constituent elements are introduced to clarify the meaning and compositional relationship of each part of the scene modelling language. Secondly, data types are defined to represent the different kinds and formats of data and to specify the form of data storage. Finally introduce word classes and keywords, and give the corresponding labels and their meanings, by designing the corresponding vocabularies in order to fully describe the scene model constructed by applying the scene modelling approach.

