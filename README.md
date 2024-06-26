# ASML
This is a document that introduces the design of Application Scenario Modeling Language (ASML), including its design objectives, lexical rules, and grammar rules.

## Preface

Based on the application scenario modelling approach, combined with the UAV swarm mission description languages SML, SML-E and GML studied in the previous research, this document designs an Application Scenario Modeling Language (ASML) for UAV swarms on the basis of which to describe the scenario models constructed by the application scenario modelling approach and reasonably characterize the scenario tasks, resources and constraint information to achieve accurate and efficient description of the applications of UAS under different scenarios. The ASML is designed to describe the scenario models constructed by the application scenario modelling approach, and to reasonably characterize the tasks, resources and constraints of the scenarios, so as to accurately and efficiently describe the applications of the UAV systems in different scenarios. In this document, the lexical and syntactic rules are determined and an extensible markup language-based approach is adopted to design an application scenario modelling language with good readability, extensibility and reusability.

## Design Goal

The design needs to be guided by the principle of achieving basic linguistic competence while reflecting the precision and specialization of the UAV swarm oriented domain. In designing ASML, this language refers to the design methodologies of other cluster task description languages such as SML, SML-E and GML.

- Needs to adapt to complex and diverse UAV swarm application scenarios, so it also needs to provide good scalability and reusability.

- Separating scenario descriptions from underlying system implementations lowers the threshold to enable rapid user interaction with a swarm of drones.

  

## Lexical Rule

In order to more accurately describe the scene model constructed by the application scene modelling approach, reasonable lexical rules are needed to carry out clear and explicit definition of the lexical rules of the elements in the application scene modelling language. These include constituent elements, data types and keywords. 

1. Firstly, the constituent elements are introduced to clarify the meaning and compositional relationship of each part of the scene modelling language. 
2. Secondly, data types are defined to represent the different kinds and formats of data and to specify the form of data storage. 
3. Finally introduce word classes and keywords, and give the corresponding labels and their meanings, by designing the corresponding vocabularies in order to fully describe the scene model constructed by applying the scene modelling approach.

### Component elements

According to the definition of the application scenario model, ASML consists of three parts: Mission Description Language, Resource Description Language and Constraint Description Language. Scenario denotes the scenario, which refers to the description of the mission, resources and constraints of the UAV swarm in a specific scenario (e.g. highway patrols). Mission is the mission of the scenario, which refers to the global mission of the scenario, Resource is the resources, which refers to the payload and UAVs that the UAV swarm has during the execution of the mission of the scenario, and Constraint is the constraints, which refers to the environmental constraints that the UAV is subjected to during the execution of the mission of the scenario. The scenario is defined in the form of a ternary.

$$
Scenario=〈Mission,Resource,Constraint〉
$$

### Data type

Data types are used to define the nature of the data and the rules for taking values, which determine the range of values that can be stored in the data. ASML includes seven data types, the specific type names and their corresponding examples are shown below:

-  **int**: integer type, such as 0, 1, -1, 77;
-  **identifier**: an identifier, consisting of a number, an underscore and a letter, and the number cannot be the first character, while the first must be a letter or an underscore. Also, it is necessary to ensure that it does not conflict with reserved keywords, such as predefined parameter names including behavioural primitives such as TAKE_OFF, LAND, etc;
- **double**: floating point number, used to represent numbers with a fractional part, e.g. 0.0, 1.5, -3.14;
-  **string**: string, consisting of multiple characters and wrapped in single or double quotes;
-  **time**: time, using the ISO8601 standard format (i.e., year-month-day T hour: minute: second form, e.g., 2023-11-23T12:30:45) to accurately represent date and time information;
- **coordinate3**: three-dimensional coordinates, including the location of the longitude, latitude and altitude, such as (122.4294, 37.7649, 50), indicating that the coordinates are located in the longitude 122.4294, latitude 37.7649, altitude 100 metres above sea level;
-  **coordinate3Array**: an array of 3D coordinates, including two or more 3D coordinates, such as {(0,0,2),(3,4,7)}, {(0,1,-1),(4,2,1),(3,6,8)}.

### Word Classes and Keywords

For the design of keywords, ASML expands lexical rules based on XML. XML's parts mainly include elements, tags, attributes and text content. Among them, elements constitute the basic structural unit of an XML document, consisting of start and end tags and content. Tags are surrounded by "< " and ">" and are used to define elements. Attributes can be added to elements to supplement additional descriptive information. Properties are in the opening tag, separated by spaces. Comments can provide explanatory text or remark information for XML documents. Comments start with "< !--" and end with "-->" and will not be processed by the parser. Tags such as "< A attribute = "value">Content< /A>" are an example of ASML and are composed of multiple parts of speech. Use this example to introduce the corresponding lexical rules.

Tab1. Name and meaning of the word class

| Word Class | Name                  | Meaning                                                     |
| :--------- | :-------------------- | :---------------------------------------------------------- |
| < A >      | Start Tag             | Indicates the beginning of the description of the element   |
| A          | Tag Name              | Indicates the name of the element                           |
| Content    | Tag Content           | Indicates the specific value of the element                 |
| < /A >     | End Tag               | Indicates the end of the description of the element         |
| Attribute  | Attribute Name        | Indicates the attribute name of the element                 |
| =          | Attribute equals sign | Used to concatenate property names and property values      |
| “”         | Quotation mark        | For wrapping attribute values                               |
| Value      | Attribute Content     | Indicates the attribute value corresponding to an attribute |
| < A/ >     | Single Tag            | Indicates an element with no tag content                    |

 The scenario tasks include the keywords Mission, Task, and SubTask, and each keyword has multiple sub-tags.

Tab 2. Keywords and sub-tags for Mission,Task and SubTask

| Keywords | Sub-tag name        |
| -------- | ------------------- |
| Mission  | MissionState        |
|          | MissionType         |
|          | MissionTime         |
|          | MissionCoord        |
|          | MissionRelationship |
|          | MissionRequirements |
| Task     | TaskState           |
|          | TaskType            |
|          | TaskTime            |
|          | TaskCoord           |
|          | TaskRelationship    |
|          | TaskRequirements    |
| SubTask  | SubTaskState        |
|          | SubTaskType         |
|          | SubTaskTime         |
|          | SubTaskCoord        |
|          | SubTaskRequirements |
|          | SubTaskBehavior     |
|          | SubTaskTarget       |

Tab 3. Keywords and sub-tags meaning of resources

| Keywords | Sub-tag name |
| -------- | ------------ |
| Resource | Info         |
|          | State        |
|          | Domain       |
|          | Performance  |
|          | Service      |
|          | Log          |

Tab 4. Constrained Keywords and Subtags

| Keywords     | Sub-tag name |
| ------------ | ------------ |
| Waypoints    | WayPoint     |
|              | Connectivity |
| Obstacle     | Obstacle     |
| NoFlyArea    | Polygon      |
|              | Rectangle    |
|              | Circle       |
|              | Coords       |
| SafeDistcane | SafeDistcane |
| Weather      | Duration     |
|              | Temperature  |
|              | CoveredArea  |
|              | Wind         |

## Grammatical rule

​      Based on the lexical rules in the previous section, this section describes the syntactic rules of ASML. The Backus-Naur Form (BNF,https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form) is used for the definition of syntactic rules for scene elements, their tasks, resources, and constraint sub-elements and attributes. BNF provides a more formalized system of syntactic description structure. As a specialized meta-language for defining languages, it is characterized by its concise syntax, clarity of expression, and ease of syntactic analysis and compilation. BNF can represent syntactic rules in a standardized way, and the syntax it presents does not depend on a specific context-free environment. Its basic structure is "< non-terminal>::= < replacement>", i.e., the left form is non-terminal, indicating that the content that has not been fully defined can be further defined and introduced by the replacement on the right. Introduction. Through XML syntax, elements, element attributes, element optionality and relationships between elements can be defined for ASML. Among them, XML Schema can be used to clarify and elaborate the structure and rules of XML documents and provide a way to define elements and their attributes to ensure the validity of document structure and content. In this paper, XML Schema diagrams are used to visualize the attributes and sub-element composition of each element in ASML. Some of the syntax rules of BNF adopted by ASML are shown in the table 5.

Tab 5. Some of the syntax rules of BNF

| Symbol | Meanings                                                     |
| ------ | ------------------------------------------------------------ |
| ::=    | Symbol for "defined as"                                      |
| < A >  | A is mandatory and must appear                               |
| “A”    | A is a term that does not need to be translated              |
| ‘A’    | A is a term that does not need to be translated              |
| [A]    | A is optional                                                |
| {A}    | A is a repeating item that can occur any number of times, including zero. |
| A*     | A is a repeating item that can occur any number of times, including zero. |
| A+     | A may occur one or more times                                |
| A \| B | A and B are tied options, only one can be chosen             |

In ASML, a scenario is defined by means of the < Scenario > element, which consists of three sub-elements, < Mission>, < Resource>, and < Constraint>. There is and can only be one < Scenario > as the root element. In it, the mission description language performs hierarchical splitting to decompose complex tasks into easy-to-solve subtasks, which are processed separately. According to the hierarchy from high to low, it mainly includes scenario , missions,tasks and subtasks. Among them, < Mission > denotes scene mission, < Task > denotes task, and < SubTask > denotes sub-task. 

Fig 1. XML Schema for the Scenario element

<div align="center">
  <img src="https://github.com/PiedPiper911/ASML/blob/main/image-20240320172517471.png?raw=true">
</div>



### Mission Syntax

In the following, the keywords, semantics and the corresponding XML Schema structure diagrams of each element of a mission in ASML will be introduced in turn, while the syntax rules for each element and its attributes will be defined.

#### Mission

A mission is defined in ASML by means of the < Mission > element, whose defined XML Schema is shown in Fig 2. The < Mission > element contains basic information such as id, name, and describe, as well as the sub-elements scenario mission property < MissionProperty > and task collection < Task>, where the < Task > element can take one or more. The < MissionProperty > element contains the sub-elements < MissionState>, < MissionType>, < MissionTime>, < MissionCoord>, < MissionRelationship>, and < MissionRequirement>, and the there is one and only one of each sub-element. The keywords in the < Mission > element are shown in Table 6.

Tab 6. < Mission>Keyword list in elements

| Keywords        | Quantities | Meaning                                    |
| --------------- | ---------- | ------------------------------------------ |
| id              | 1          | Unique identifier for the scenario mission |
| name            | 1          | Name of the scenario mission               |
| describe        | 1          | Description of the scenario mission        |
| MissionProperty | 1          | Properties of scenario missions            |
| Task            | 1 or more  | Tasks in missions                          |

The values of the elements and attributes in < Mission > are restricted by syntax rules. In particular, < MissionState_value > is of type string and is restricted to one of "Allocated", "Unallocated" or "PartiallyAllocated". The < MissionType_value > is of type string and is restricted to one of "Logistics", "Agriculture", "Rescue", and "HighwayPatrol". The < MissionTime > element includes the < StartTime>, < EndTime>, and < EstimatedTime > child elements. The < MissionCoord > element contains the < EnterPoint > and < LeavePoint > child elements. The < MissionRelationship > takes the value of one of < Sequence>, < CoBegin>, < Fork>, or < Join>. < MissionRequirement > contains one or more < ResourceType > child elements.

Table 7 lists the syntax rules for the major elements and attributes of < Mission>.

Tab 7.  Syntax rules for < Mission > child elements and attributes

| Non-terminal            | Symbol | Replacement                                                  |
| ----------------------- | ------ | ------------------------------------------------------------ |
| < Mission >             | ::=    | < MissionProperty>< Task>+                                   |
| < MissionProperty >     | ::=    | < MissionState>< MissionType>< MissionTime>< MissionCoord >  < MissionRelationship>< MissionRequirement > |
| < MissionState_value >  | ::=    | "Allocated" \|  "Unallocated" \| "PartiallyAllocated"        |
| < MissionType_value >   | ::=    | "Logistics" \|  "Agriculture" \| "Rescue" \| "HighwayPatrol" |
| < MissionTime >         | ::=    | < StartTime>< EndTime>< EstimatedTime >                      |
| < MissionCoord >        | ::=    | < EnterPoint>< LeavePoint >                                  |
| < MissionRelationship > | ::=    | < Sequence > \| < CoBegin > \|  < Fork > \| < Join >         |
| < MissionRequirement >  | ::=    | < ResourceType>+                                             |

Fig 2. XML Schema for the Mission element

<div align="center">
  <img src="https://github.com/PiedPiper911/ASML/blob/main/image-20240320194406066.png?raw=true">
</div>

#### Task

A task is defined in ASML by means of the < Task > element, whose defined XML Schema is shown in Fig 3. The < Task > element contains basic information such as id, name, and describe, as well as the sub-elements < TaskProperty > and the collection of subtasks < SubTask>, where the < SubTask > element can take one or more. The < TaskProperty > element contains the sub-elements < TaskState>, < TaskType>, < TaskTime>, < TaskCoord>, < TaskRelationship>, and < TaskRequirement>, and there is one and only one of each of these sub-elements. According to the definition of the meta-model, the attributes in < Task > are the same as those in < Mission>, only the sub-elements are different, as shown in Table 8.

Tab 8.  Table of child elements in the < Task > element

| Sub-element  | Quantities | Meaning                |
| ------------ | ---------- | ---------------------- |
| TaskProperty | 1          | Properties of the task |
| SubTask      | 1 or more  | Subtasks within a task |

The values of the elements and attributes in < Task > are restricted by syntax rules. According to the metamodel's definition of the TaskType relationship, the type of a child task is restricted by the type of the parent task. When < MissionType_value > is "Logistics", < TaskType_value > can be "TansportTask" or "DistributeTask"; when < MissionType_value > is "Agriculture", < TaskType_value > can be "TansportTask" or "DistributeTask". value > can be "SprayingTask" or "InspectionTask"; when < MissionType_value > is "Rescue", < TaskType_value > can be "SearchTask", "TansportTask" or "CommunicationTask". CommunicationTask"; when < MissionType_value > is "HighwayPatrol", < TaskType_value > can be "RoadTask", "SlopeTask" or "BridgeTask". In addition, the rules for < TaskState>, < TaskTime>, < TaskCoord>, < TaskRelationship>, and < TaskRequirement > are the same as the syntax rules in < Mission>, so we won't go into detail here. 

Tab 9. < Task > Syntax rules for child elements and attributes

| Non-terminal       | **Symbol** | **Replacement**                                              |
| ------------------ | ---------- | ------------------------------------------------------------ |
| < Task >           | ::=        | < TaskProperty>< SubTask>+                                   |
| < TaskProperty >   | ::=        | < TaskState>< TaskType>< TaskTime>< TaskCoord >  < TaskRelationship>< TaskRequirement > |
| <TaskState_value>  | ::=        | "Allocated"  \| "Unallocated" \| "PartiallyAllocated"        |
| < TaskType_value > | ::=        | < Logistics >  if < MissionType_value > = "Logistics  \|  < Agriculture > if < MissionType_value > = "Agriculture"  \|  < Rescue > if < MissionType_value > = "Rescue"  \|  < HighwayPatrol > if < MissionType_value > =  "HighwayPatrol" |
| < Logistics >      | ::=        | "TansportTask"  \| "DistributeTask"                          |
| < Agriculture >    | ::=        | "SprayingTask  " \| "InspectionTask"                         |
| < Rescue >         | ::=        | "SearchTask"  \| "TansportTask" \| "CommunicationTask"       |
| < HighwayPatrols > | ::=        | "RoadTask"  \| "SlopeTask" \| "BridgeTask"                   |

Fig 3. XML Schema for the Task element

<div align="center">
  <img src="https://github.com/PiedPiper911/ASML/blob/main/image-20240320201405678.png?raw=true">
</div>



#### SubTask

In ASML, a subtask is defined through the < SubTask > element, and the XML Schema defined is shown in Fig 4. The < SubTask > element contains basic information such as id, name and describe, as well as the sub-element subtask attribute < SubTaskProperty >. Similar to < MissionProperty > and < TaskProperty >, the < SubTaskProperty > element contains the sub-elements < SubTaskState >, < SubTaskType >, < SubTaskTime >, < SubTaskCoord > and < SubTaskRequirement >. According to the definition of the metamodel, subtasks serve as terminal tasks, and additional < SubTaskTarget> and < SubTaskBehavoir > are included in the subelements. The attributes in < SubTask > are consistent with those of < Mission > and < Task >, but the child elements only contain < SubTaskProperty >. The sub-elements of < SubTaskProperty > are shown in Tab 10.

Tab 10.Subelements in the < SubTaskProperty > element

| Keywords           | Specific to terminal tasks | Meanings                |
| ------------------ | -------------------------- | ----------------------- |
| SubTaskState       | ×                          | State of subTasks       |
| SubTaskType        | ×                          | Type of subTasks        |
| SubTaskTime        | ×                          | Time of subTasks        |
| SubTaskCoord       | ×                          | Coord of subTasks       |
| SubTaskRequirement | ×                          | Requirement of subTasks |
| SubTaskTarget      | √                          | Target of subTasks      |
| SubTaskBehavior    | √                          | Behavior of subTasks    |

The values of each element and attribute in < SubTask > are restricted by syntax rules. According to the task Type relationship definition of the metamodel, the type of child tasks is restricted by the type of the parent task. The state value of SubTask is represented by <SubTaskState_value>. The value is of string type and is limited to one of "Allocated" or "Unallocated". The task type of a SubTask is limited by the task type of the Task, so < SubTaskType > includes one of the sub-elements < SubLogistics >, < SubAgriculture >, < SubRescue > or < SubHighwayPatrols >. In addition, the rules of < SubTaskTime >, < SubTaskCoord > and < SubTaskRequirement > are the same as the corresponding syntax rules in < Mission > and < Task >, and will not be introduced in detail here. Some syntax rules for < SubTask > subelements and attributes are shown in Tab 11.

Tab 11. Some syntax rules for < SubTask > subelements and attributes

| Non-terminal          | Symbol | Replacement                                                  |
| --------------------- | ------ | ------------------------------------------------------------ |
| < SubTask >           | ::=    | < SubTaskProperty >                                          |
| < SubTaskProperty >   | ::=    | < SubTaskState >< SubTaskType >< SubTaskTime >  < SubTaskCoord >< SubTaskRequirement >  < SubTaskTarget >< SubTaskBehavior> |
| <SubTaskState_value>  | ::=    | "Allocated" \| "Unallocated"                                 |
| <SubTaskType_value>   | ::=    | < SubLogistics > \| < SubAgriculture > \|  < SubRescue > \| < SubHighwayPatrols > |
| < SubHighwayPatrols > | ::=    | < Road > if <TaskType_value> =  "RoadTask"  \| < Bridge > if <TaskType_value> =  "BridgeTask"  \| < Slope > if <TaskType_value> =  "SlopeTask" |
| < Road >              | ::=    | " RoadBarrier " \| " RoadGuardarail  " \| " RoadSurface"     |
| < Bridge >            | ::=    | " BridgeDeck " \| "BridgeBearing " \|  "BridgePier" \| " BridgeJoint" \|"BridgeAbutment" |
| < Slope >             | ::=    | "SlopeBottom" \| "SlopeSurface" \|  "SlopeDitch"             |
| < SubTaskTarget >     | ::=    | < TargetLocation >< TargetType >< TargetShape >  < TargetEvent >< TargetSize >< TargetCoords > |
| < TargetLocation >    | ::=    | < Coord >                                                    |
| <TargetType_value>    | ::=    | "Point" \| "Line" \|  "Surface" \| "3D"                      |
| <TargetShape_value>   | ::=    | "Cube" \| "Cylinder"                                         |
| <TargetEvent_value>   | ::=    | "TAKE_PHOTO" \| "FILM_VIDEO" \|  "LIGHTING" \| < OtherEvents > |
| < TargetSize >        | ::=    | < CubeSize > if <TargetShape_value > =  "Cube" \|  < CylinderSize > if < TargetShape_value > =  "Cylinder" |
| < TargetCoords >      | ::=    | < TargetCoord >                                              |
| < SubTaskBehavior >   | ::=    | < Behavior >+                                                |

Fig 4. XML Schema of SubTask element

<div align="center">
  <img src="https://github.com/PiedPiper911/ASML/blob/main/image-20240321203126361.png?raw=true">
</div>



### UAV Resource Capability Syntax

#### Resource

A resource is defined in ASML through < Resource>. A < Resource > contains sub-elements < Info>, < State>, < Domain>, < Performance>, < Service>, and < Log>. The XML schema for the Resource element is shown in Fig 5.

Fig 5. XML Schema for Resource elements

<div align="center">
  <img src="https://github.com/PiedPiper911/ASML/blob/main/image-20240320202028819.png?raw=true">
</div>

#### Performance

The performance information of a resource is defined in ASML through the < Performance>, which demonstrates different capabilities depending on the UAV resource, and which has one or more sub-elements, as shown in Fig 6. The syntax of each of these tags to take values is mainly in the form of strings or floating point numbers and will not be repeated here.

Fig 6. XML structure diagram for resource performance

<div align="center">
  <img src="https://github.com/PiedPiper911/ASML/blob/main/image-20240320202331886.png?raw=true">
</div>

###  Environmentally Constrained Syntax

#### Constraint

A constraint is defined in ASML through < Constraint>. Its sub-elements include path points < WayPoints>, < Obstacle>, < NoFlyArea>, < SafeDistance>, and < Weather>. The XML Schema composed of its sub-elements is shown in Fig 7.

Fig 7. XML Schema for Constraint Elements

<div align="center">
  <img src="https://github.com/PiedPiper911/ASML/blob/main/image-20240320202750422.png?raw=true">
</div>



#### Waypoints

The < Waypoints > contains one or more child elements < Waypoint>, as shown in Fig 8. The < Waypoint > element includes the attributes id, longitude, latitude, and altitude, and has a unique child element, < Connectivity>, which serves as a representation of connectivity with other Waypoints, and takes the value of a string of 0s and 1s, and the length of the number of child elements of < Waypoints>. The syntax rules for the < Waypoints > element and attributes are defined in Tab 12.

Tab 12 . Syntax rules for < WayPoints > child elements and attributes

| Non-terminal           | **Symbol** | Replacement                                          |
| ---------------------- | ---------- | ---------------------------------------------------- |
| < WayPoints >          | ::=        | < WayPoint>+                                         |
| < Waypoint >           | ::=        | < Connectivity >                                     |
| < Waypoint_attr >      | ::=        | < WayPoint_id>< Coord_attr >                         |
| < Connectivity >       | ::=        | < Connectivity_value > (","  < Connectivity_value>)* |
| < Connectivity_value > | ::=        | "0" \| "1"                                           |

Fig 8 XML Schema for the WayPoints element

<div align="center">
  <img src="https://github.com/PiedPiper911/ASML/blob/main/image-20240320203246363.png?raw=true">
</div>

#### Obstacle

The < Obstacle > contains the attributes id, name, and the coordinates longitude and latitude in Coord, and the child elements < minAlt > and < maxAlt>, as shown in Fig 9. Obstacles describes objects in terms of height that the UAV may not penetrate or touch. Where < minAlt > and < maxAlt > are the same as the < Coord_attr > rule defined earlier, taking the value of double precision floating point number double.

Fig 9.XML Schema for the Obstacle element.

<div align="center">
  <img src="https://github.com/PiedPiper911/ASML/blob/main/image-20240320203409599.png?raw=true">
</div>



#### NoFlyArea

The no-fly area is represented by the < NoFlyArea > element, whose sub-element composition is shown in Fig 10, with < Circle>, < Rectangle>, and < Polygon > as its optional sub-elements. The sub-elements of polygon < Coords > have at least three coordinates, indicating that it consists of three and more coordinate points. The syntax rules for each child element and attribute of < NoFlyArea > are shown in Tab 13.

Tab 13 Syntax rules for < NoFlyArea > child elements and attributes

| Non-terminal  | Symbol | Replacement                                  |
| ------------- | ------ | -------------------------------------------- |
| < Rectangle > | ::=    | < Center > (< NE > < SW>) \|  (< NW > < SE>) |
| < Circle >    | ::=    | < Center>< Radius >                          |
| < Polygon >   | ::=    | < Coords >                                   |
| < Coords >    | ::=    | (< Coord>< Coord>)< Coord>+                  |

Fig 10. XML Schema for the NoFlyArea element

<div align="center">
  <img src="https://github.com/PiedPiper911/ASML/blob/main/image-20240320203948652.png?raw=true">
</div>

**SafeDistance**

The safe distance is represented by the < SafeDistance > element, containing the attributes id, name, and the sub-elements minimum safe distance < minDis>, minimum and maximum flight altitude < minAlt>, and < maxAlt>. < minAlt > and < maxAlt > are defined with the same rules as in < Obstacle>, while < minDis > takes the value of a string. The structure of its elements is shown in Fig 11.

Fig 11.XML Schema of the SafeDistance element
<div align="center">
  <img src="https://github.com/PiedPiper911/ASML/blob/main/image-20240320204331478.png?raw=true">
</div>

#### Weather

Weather is represented through the < Weather > element with attributes id, name, describe, and type. it contains sub-elements Duration < Duration>, Temperature Range < Temperature>, Covered Area < CoveredArea>, and Wind < Wind>. The value of < Durtaion > needs to be restricted to the ISO8601 date representation, covering the start and end time < DateTime>, connected by the "~" symbol. The value of < Temperature > is in the form of "20℃~30℃", indicating the temperature range. < CoveredArea > is the same as < NoFlyArea>. < Wind > contains sub-elements < WindLevel > and < WindSpeed > with integer and string values respectively. The XML schema for the < Weather > element is shown in Fig 12.



Fig 12.XML Schema for the Weather Element

<div align="center">
  <img src="https://github.com/PiedPiper911/ASML/blob/main/image-20240320204426904.png?raw=true">
</div>



## Conclusion

This document mainly accomplishes the design of the Application Scenario Modeling Language (ASML). Firstly, the main steps of constructing the Application Scenario Modeling Language are elicited based on the design objectives and approach. Secondly formulate the lexical rules including constituent elements, data types and keywords, and define the syntax rules for the three main parts of the scenario mission, UAV resources, and environmental constraints. Finally, the composition of the elements and attributes are described by means of an extensible markup language-based approach, and an XML schema diagram is given to represent the compositional relationships between the elements.



## Example for ASML

### Highway patrol Mission

This XML file describes the scenario of a highway inspection task, including the time, location, type of the task, and the specific execution of sub-tasks, including inspection and photography tasks for bridges and piers.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<! -- Example for highway inspection mission -->
<Mission id="1" name="Highway" describe="Patrols of highway">
  <MissionProperty>
    <MissionState>Allocated</MissionState>
    <MissionType>HighwayPatrols</MissionType>
    <MissionTime>
      <StartTime>2023-12-28T22:02:08</StartTime>
      <EndTime>2023-12-28T23:02:08</EndTime>
      <EstimatedTime>30min</EstimatedTime>
    </MissionTime>
    <MissionCoord>
      <EnterPoint longitude="10" latitude="60" altitude="60" />
      <LeavePoint longitude="90" latitude="60" altitude="60" />
    </MissionCoord>
    <MissionRelationship />
    <MissionRequirements />
  </MissionProperty>
  <Task id="0" name="task_1" describe="This is a default description">
    <TaskProperty>
      <TaskState>Allocated</TaskState>
      <TaskType>BridgeTask</TaskType>
      <TaskTime>
        <StartTime>2023-12-28T22:02:14</StartTime>
        <EndTime>2023-12-28T23:02:14</EndTime>
        <EstimatedTime>30min</EstimatedTime>
      </TaskTime>
      <TaskCoord>
        <EnterPoint longitude="10" latitude="60" altitude="60" />
        <LeavePoint longitude="90" latitude="60" altitude="60" />
      </TaskCoord>
      <TaskRelationship />
      <TaskRequirements />
    </TaskProperty>
    <SubTask id="0" name="subTask_1" describe="This is a default description">
      <SubTaskProperty>
        <SubTaskState>Allocated</SubTaskState>
        <SubTaskType>BridgePier</SubTaskType>
        <SubTaskTime>
          <StartTime>2023-12-28T22:06:17</StartTime>
          <EndTime>2023-12-28T23:06:17</EndTime>
          <EstimatedTime>30min</EstimatedTime>
        </SubTaskTime>
        <SubTaskCoord>
          <EnterPoint longitude="20" latitude="20" altitude="5" />
          <LeavePoint longitude="40" latitude="20" altitude="5" />
        </SubTaskCoord>
        <SubTaskTarget id="0" name="subTask_1">
          <TargetLocation longitude="20" latitude="20" altitude="5" />
          <TargetType>3D</TargetType>
          <TargetShape>cube</TargetShape>
          <TargetEvent>PHOTO</TargetEvent>
          <TargetCoords>
            <TargetCoord longitude="35" latitude="25" altitude="30" />
            <TargetCoord longitude="35" latitude="20" altitude="30" />
            <TargetCoord longitude="30" latitude="20" altitude="30" />
            <TargetCoord longitude="30" latitude="25" altitude="30" />
            <TargetCoord longitude="35" latitude="25" altitude="0" />
            <TargetCoord longitude="35" latitude="20" altitude="0" />
            <TargetCoord longitude="30" latitude="20" altitude="0" />
            <TargetCoord longitude="30" latitude="25" altitude="0" />
          </TargetCoords>
        </SubTaskTarget>
        <SubTaskBehavior>TAKE_PHOTO</SubTaskBehavior>
      </SubTaskProperty>
    </SubTask>
  </Task>
</Mission>

```



### Logistics Mission

This scenario describes a logistics task, divided into two main tasks:

 Task 1: Loading task 

- It starts at 17:21:40 on December 1, 2023, and ends at 18:21:40, and is expected to last 5 minutes. 
- Load cargo from the location of longitude 108.885473, latitude 34.193698.
- The cargo is loaded to the location of longitude 108.884085 and latitude 34.193800. 
- The loading point shape is a cylinder with a height of 0 and a radius of 0. 

Task 2: Transport Task 

- It will start at 17:22 on December 1, 2023, end at 18:22, and is expected to last 20 minutes. 
- Depart from the location of longitude 108.883882, latitude 34.193825, and transport to the location of longitude 108.870495, latitude 34.193784. 
- The shape of the transportation line is a cube with a height of 0 and a radius of 0. 
- This scenario describes the logistics task of loading and transporting goods at a specified time and place.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<! -- Example of a logistics and transportation scenario task -->
<Mission id="0" name="mission_0" describe="default">
  <MissionProperty>
    <MissionState>Allocated</MissionState>
    <MissionType>Logistics</MissionType>
    <MissionTime>
      <StartTime>2023-12-01T17:21:08</StartTime>
      <EndTime>2023-12-01T18:21:08</EndTime>
      <EstimatedTime>30min</EstimatedTime>
    </MissionTime>
    <MissionCoord>
      <EnterPoint longitude="108.885" latitude="34.1938" altitude="10" />
      <LeavePoint longitude="108.871" latitude="34.1939" altitude="10" />
    </MissionCoord>
    <MissionRelationship>
      <Sequence Tasks="task1,task2" />
    </MissionRelationship>
    <MissionRequirements />
  </MissionProperty>
  <Task id="0" name="task_1" describe="This is a default description">
    <TaskProperty>
      <TaskState>Allocated</TaskState>
      <TaskType>LoadingTask</TaskType>
      <TaskTime>
        <StartTime>2023-12-01T17:21:40</StartTime>
        <EndTime>2023-12-01T18:21:40</EndTime>
        <EstimatedTime>5min</EstimatedTime>
      </TaskTime>
      <TaskCoord>
        <EnterPoint longitude="108.885473" latitude="34.193698" altitude="10" />
        <EnterPoint longitude="108.884085" latitude="34.193800" altitude="10" />
      </TaskCoord>
      <TaskRelationship />
      <TaskRequirements />
    </TaskProperty>
    <SubTask id="0" name="load_subtask" describe="This is a default description">
      <SubTaskProperty>
        <SubTaskState>Allocated</SubTaskState>
        <SubTaskType>CargoLoading</SubTaskType>
        <SubTaskTime>
          <StartTime>2023-12-01T17:21:40</StartTime>
          <EndTime>2023-12-01T18:21:40</EndTime>
          <EstimatedTime>5min</EstimatedTime>
        </SubTaskTime>
        <SubTaskCoord>
          <EnterPoint longitude="108.8854" latitude="34.1936" altitude="10" />
          <EnterPoint longitude="108.8840" latitude="34.1938" altitude="10" />
        </SubTaskCoord>
        <SubTaskTarget id="0" name="load_point">
          <TargetLocation longitude="108.8840" latitude="34.1938" altitude="10" />
          <TargetType>point</TargetType>
          <TargetShape>cylinder</TargetShape>
          <TargetEvent>LOAD</TargetEvent>
          <TargetSize>
            <Height>0.000000</Height>
            <Radius>0.000000</Radius>
            <Center>108.885,34.1938,0</Center>
          </TargetSize>
          <TargetCoords />
        </SubTaskTarget>
        <SubTaskBehavior>LOAD</SubTaskBehavior>
      </SubTaskProperty>
    </SubTask>
  </Task>
  <Task id="1" name="task_2" describe="This is a default description">
    <TaskProperty>
      <TaskState>Allocated</TaskState>
      <TaskType>TransportTask</TaskType>
      <TaskTime>
        <StartTime>2023-12-01T17:22:00</StartTime>
        <EndTime>2023-12-01T18:22:00</EndTime>
        <EstimatedTime>20min</EstimatedTime>
      </TaskTime>
      <TaskCoord>
        <EnterPoint longitude="108.883882" latitude="34.193825" altitude="10" />
        <LeavePoint longitude="34.193786" latitude="108.883532" altitude="10" />
      </TaskCoord>
      <TaskRelationship />
      <TaskRequirements />
    </TaskProperty>
    <SubTask id="1" name="transport_subtask" describe="This is a default description">
      <SubTaskProperty>
        <SubTaskState>Allocated</SubTaskState>
        <SubTaskType>CargoTransport</SubTaskType>
        <SubTaskTime>
          <StartTime>2023-12-01T17:21:40</StartTime>
          <EndTime>2023-12-01T18:21:40</EndTime>
          <EstimatedTime>20min</EstimatedTime>
        </SubTaskTime>
        <SubTaskCoord>
          <EnterPoint longitude="108.883224" latitude="34.193889" altitude="10" />
          <EnterPoint longitude="108.870495" latitude="34.193784" altitude="10" />
        </SubTaskCoord>
        <SubTaskTarget id="1" name="transport_line">
          <TargetLocation longitude="108.870495" latitude="34.193784" altitude="10" />
          <TargetType>line</TargetType>
          <TargetShape>cube</TargetShape>
          <TargetEvent>TRANSPORT</TargetEvent>
          <TargetSize>
            <Height>0.000000</Height>
            <Radius>0.000000</Radius>
            <Center>108.870495,34.193784,10</Center>
          </TargetSize>
          <TargetCoords />
        </SubTaskTarget>
        <SubTaskBehavior>TRANSPORT</SubTaskBehavior>
      </SubTaskProperty>
    </SubTask>
  </Task>
</Mission>
```



### Resource

This XML file generally describes a resource, which is a drone. It provides basic information, status, domain, performance parameters, service time and other information of resources. The performance parameters include mobility, perception, communication, load capacity and endurance. These parameters cover the resource’s capabilities in movement, perception, communication, carrying payloads and continuous flight. The log information of the resource is also recorded, including the recording time and related remarks.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Resource>
  <Info id="1" name="example" type="test" description="this is an example" />
  <State>FullLoad</State>
  <Domain>Logistics, Agriculture, Rescue</Domain>
  <Perfomance>
    <MoveAbility>
      <maxAscendingSpeed>16.000000</maxAscendingSpeed>
      <maxDescendingSpeed>23.000000</maxDescendingSpeed>
      <maxHorizontalSpeed>25.000000</maxHorizontalSpeed>
      <maxWindResistance>12</maxWindResistance>
      <maxTakeoffAltitude>1000</maxTakeoffAltitude>
      <maxTiltAngle>30.0</maxTiltAngle>
      <maxRotationSpeed>15</maxRotationSpeed>
      <maxHoveringTime>30min</maxHoveringTime>
    </MoveAbility>
    <SenseAbility>
      <senseAbilityType>
        MonocularVision
      </senseAbilityType>
      <obstacleAvoidanceDirection>
        <FrontView SenseDistance="0.5-20" DetectableRange="5.0" AvoidanceSpeed="10.0" FOV="(45,60)" />
        <RearView SenseDistance="0.5-20" AvoidanceSpeed="10.0" FOV="(60,60)" />
        <SideView SenseDistance="0.5-20" AvoidanceSpeed="10.0" FOV="(30,90)" />
      </obstacleAvoidanceDirection>
    </SenseAbility>
    <CommunicationAbility>
      <GNSS>GPS+BeiDou</GNSS>
      <workingFrequency>5.8GHz</workingFrequency>
      <maxSignalRange>10.5km</maxSignalRange>
      <imageTransmission>
        <imageQuality>1080P@30fps</imageQuality>
        <imageDelay>100ms</imageDelay>
      </imageTransmission>
    </CommunicationAbility>
    <PayloadAbility>
      <emptyWeight>2.5kg</emptyWeight>
      <takeoffWeight>4kg</takeoffWeight>
      <maxPayload>1.5kg</maxPayload>
      <maxPayloadEndurance>20min</maxPayloadEndurance>
      <gimbalQuantity>1</gimbalQuantity>
    </PayloadAbility>
    <EnduranceAbility>
      <maxFilghtRange>10.5km</maxFilghtRange>
      <flightTime>25.3min</flightTime>
      <currentFlightTime>20min</currentFlightTime>
      <remainingFlightTime>5.3min</remainingFlightTime>
      <workingTemperature>25℃</workingTemperature>
      <protection>ip45</protection>
    </EnduranceAbility>
  </Perfomance>
  <Service Number="1" Time="10:00:00-12:00:00" />
  <Log Time="2023-12-28T10:30:00" Note="Started mission." />
</Resource>

```

### Constraint

This XML describes a series of constraints that can be used in drone flights or similar applications:

- WayPoints elements: Describes a series of waypoints, each with a unique ID, longitude, latitude, and altitude, as well as connectivity to other waypoints. Obstacle elements:

- Obstacle elements: Describes the obstacle, including its ID, name, location, and minimum and maximum height. NoFlyArea element

- NoFlyArea element: No-fly zones are described, including the location and height range of polygonal, rectangular, and circular no-fly zones.

- SafeDistance element: Safety distances are described, including minimum distances and minimum and maximum heights. Weather element:

- Weather element:Weather conditions are described, including parameters such as weather type, duration, temperature range, coverage area, and wind speed.

   These constraints can be used for flight path planning, flight area restrictions and flight condition judgment to ensure safety and compliance during flight.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<Constraint>
    <WayPoints>
       <WayPoint id="WP001" longitude="108.6970" latitude="34.1297" altitude="100">
            <Connectivity>0,1,0,1</Connectivity>
        </WayPoint>
        <WayPoint id="WP002" longitude="108.7553" latitude="34.1538" altitude="150">
            <Connectivity>1,0,0,1</Connectivity>
        </WayPoint>
        <WayPoint id="WP003" longitude="108.7972" latitude="34.1720" altitude="200">
            <Connectivity>0,0,0,0</Connectivity>
        </WayPoint>
        <WayPoint id="WP004" longitude="108.8340" latitude="34.1974" altitude="250">
            <Connectivity>1,1,0,0</Connectivity>
        </WayPoint>
    </WayPoints>
    <Obstacle id="1" name="obstacle1" longitude="108.7723" latitude="34.1617">
        <minAlt>10.0</minAlt>
        <maxAlt>20.0</maxAlt>
    </Obstacle>
    <NoFlyArea>
        <Polygon id="p1" name="Polygon 1" minAlt="10" maxAlt="50">
            <Coords>
                <Coord longitude="108.6935" latitude="34.1881" altitude="20" />
                <Coord longitude="108.8253" latitude="34.1940" altitude="25" />
                <Coord longitude="108.8217" latitude="34.1145" altitude="30" />
                <Coord longitude="108.6904" latitude="34.1060" altitude="20" />
            </Coords>
        </Polygon>
        <Rectangle id="01 " name="Rect1" minAlt="10.5" maxAlt="50.2">
            <Center longitude="108.75" latitude="34.1470" altitude="25.6789" />
            <NE longitude="108.7328" latitude="34.1614" />
            <SW longitude="108.7691" latitude="34.1335" />
        </Rectangle>
        <Circle id="c1" name="Circle 1" minAlt="10" maxAlt="50">
            <Center longitude="108.7437" latitude="34.1434" altitude="20" />
            <Radius>25</Radius>
        </Circle>
    </NoFlyArea>
    <SafeDistance id="sd1" name="Safe Zone">
        <minDis>10.0</minDis>
        <minAltitude>100.0</minAltitude>
        <maxAltitude>200.0</maxAltitude>
    </SafeDistance>
    <Weather id="w001" name="Sunny" describe="Clear blue sky" type="heat">
        <Duration>2023-12-28T08:00:00~2023-12-28T18:00:00</Duration>
        <Temperature>20°C~30°C</Temperature>
        <CoveredArea>
            <Rectangle id="r001" name="City" minAlt="0" maxAlt="100">
                <Center longitude="108.8000" latitude="34.1748" altitude="0" />
                <NE longitude="108.7860" latitude="34.1784" />
                <SW longitude="108.8064" latitude="34.1675" />
            </Rectangle>
        </CoveredArea>
        <Wind>
            <WindLevel>5</WindLevel>
            <WindSpeed>20.3m/s</WindSpeed>
        </Wind>
    </Weather>
</Constraint>
```



