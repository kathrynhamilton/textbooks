# SysML

May 30, 2018 to June 1, 2018

**www.nomagic.com/support/quick-reference-guides.html**

## Model Based Systems Engineering

What does a system model do?

- Specifies a system
- Captures a logical relationship among requirements, design, analysis, verification
- NOT an analytical model to perform computation

Advantages to model based design:

- Changes are propogated to all diagrams
- Elements removed from a diagram remain in the model
- Elements removed from the model are removed from all diagrams
- Reusable design repository that can generate many types of artifacts
- Enhances traceability and ability to assess impact of proposed changes

## Types of Diagrams

-[Structure Diagrams](#stdiag)
  - [Block Definition Diagram](#bddiag)
  - [Internal Block Diagram](#ibdiag)
    - [Parametric Diagram](#pmdiag)
  - [Package Diagram](#pdiag)
- [Behavior Diagrams](#bhdiag)
  - [Activity Diagram](#atdiag)
  - [Sequence Diagram](#sqdiag)
  - [State Machine Diagram](#smdiag)
  - [Use Case Diagram](#ucdiag)
- [Requirement Diagram](#rqdiag)

Not all of these are typically necessary to model a system. Only create something if you see value in it. There is also no one good order in which to create diagrams.

![SysML Diagrams](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEngineering/images/smldiag.png "Caption")

### <a name="stdiag"></a>Structure Diagrams 

#### <a name="pdiag"></a>Package Diagram 

- Organizes model and elements
- View system from multiple levels of abstraction
- Describes dependencies between *packages* and elements

![Package Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEngineering/images/pdiag.png "Quick Reference Guide: Package Diagram")

#### <a name="bddiag"></a>Block Definiton Diagram

- Represent structure and features of system using *blocks*
- Shows *block* properties and values
- Describes relationships between *blocks*

![Block Definition Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEngineering/images/bddiag.png "Quick Reference Guide: Block Definition Diagram")

#### <a name="ibdiag"></a>Internal Block Diagram 

- Describes internal structure of a *block*
- Contains *parts*, *ports*, and *connectors*

![Internal Block Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEngineering/images/ibdiag.png "Quick Reference Guide: Internal Block Diagram")

#### <a name="pmdiag"></a>Parametric Diagram 

- Models system constraints
- Represents a usage of constraints in an specific context
- Created within a block (internal block diagram)
- Uses equation blocks (block definition diagram)

![Parametric Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEngineering/images/pmdiag.png "Quick Reference Guide: Parametric Diagram")

### <a name="bhdiag"></a>Behaviour Diagrams 

#### <a name="ucdiag"></a>Use Case Diagram 

- Describe functionality, context, and measurable value provided by system
- Contains *actors*, *use cases*, and relationships

![Use Case Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEngineering/images/ucdiag.png "Quick Reference Guide: Use Case Diagram")

#### <a name="smdiag"></a>State Machine Diagram 

- Represents a block's life cycle, using *states* and *nodes*
- Defines system behaviour as a sequence of states a component experience in response to events
- Can be brief or detailed, as required
- Describes state enter/exit conditions (optional)

![State Machine Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEngineering/images/smdiag.png "Quick Reference Guide: State Machine Diagram")

#### <a name="atdiag"></a>Activity Diagram 

- Shows a procedural flow of system behaviour, in particular the responsibilities of each actor
- Useful for workflow modeling
- Contains *actions*, *objects*, and *nodes*
- Shows evolution of the system over time

![Activity Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEngineering/images/atdiag.png "Quick Reference Guide: Activity Diagram")

#### <a name="sqdiag"></a>Sequence Diagram 

- Decribes how a group of objects performs a process, using sequential interactions
- Shows the communication and interaction between actors
- Assigns responsibilities to blocks
- Shows evolution of the system over time

![Sequence Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEngineering/images/sqdiag.png "Quick Reference Guide: Sequence Diagram")

### <a name="rqdiag"></a>Requirements Diagram 

- Describes textual requirements contained in a specification
- Shows relationships between requirements and to other model elements
- Can also be viewed as a table or matrix
- Should be organized by abstraction level

Client and Supplier elements can be used to show dependence.

Use comments to document rationale.

Relationships: (to other elements) satisfy, verify, refine, (to other requirements) derive, copy, trace, containment

Requirement Types: functional, interface, design constraint, performance, physical

![Requirements Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEngineering/images/rqdiag.png "Quick Reference Guide: Requirements Diagram")

## Methods and Frameworks

SysML is not a framework or a method. It is a language.

In order to use SysML successfully, teams need agreement on model structure and required artifacts.

A proposed framework (Magic Grid):

![Magic Grid](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEngineering/images/mg.png "Magic Grid Framework")

C1. Stakeholder Needs

- Information gathered from stakeholders
- Primary user requirements, government regulations, policies, procedures

C2. Use Cases

- Use Case Diagram
- Define measurable value provided to user
- Define system contexts where use cases are performed
- How system interacts with user in a flow of actions and events

C3. System Context

- Internal Block Diagram
- How system interacts with actors and external environment
- Define high-level interfaces needed for system to communicate with environment

C4-P4. Measurements of Effectiveness

- Block Definition Diagram (C4 - full system, P4 - subsystem)
- How well a system (or subsystem) carries out a task within a specific context
- Non-functional stakeholder needs or objectives expressed in numerical format
- Key performance indicators

P1. System Requirements

- Requirements Diagram
- Goals: long term and global achievements
- Objectives: specific, quantifiable, time-bound strategies to attain goals

P2. Functional Analysis

- Activity Diagram
- Sequence Diagram
- Continuation of use case analysis
- Focus on internal system functions
- Identification of logical subsystems

P3. Logical Subsystem Communication

- Block Definition Diagram
- Identify and define logical interfaces between logical subsystems

S1. Component Requirements

- Requirements Diagram
- Detailes requirements
- Subsstem requirements derived from system requirements
- Compoment requirements from subsystem requirements

S2. Component Behaviour

- State Machine Diagram
- Detailed behaviour of a system or subsystem
- Defines states and actions

S3. Component Assembly

- Block Definition Diagram
- Internal Block Diagram
- Show physical connections based on physical interfaces between systems, subsystems, components
- Physical components implement logical subsystems
- Does NOT include physical component detailed design

S4. Component Parameters

- Physical characteristics of a system or subsystem
- Dependencies between physical characteristics
- How physical characteristics achieve MoEs

## Packages and Model Structure

System Architecture and System Model Architecture are two different things!

There are four package types in SysML:

- Models, root of the system model
- Libraries, set of model elements intended for reuse (eg. signals, value types, interfaces, constraints, common blocks)
- Profile Packages, contains sterotypes which extend existing model elements by adding new properties, constraints, or semantics
- Views, filtered subset of the system model

Common practice is to structure based on abstraction level and framework.

Packages create unique namespace for contained model elements.
