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

SysML is not a framework or a method. It is a language.

## Types of Diagrams

- [Structure Diagrams](#stdiag)
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

![SysML Diagrams](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEnginering/images/smldiag.png "Caption")

### <a name="stdiag"></a>Structure Diagrams 

#### <a name="pdiag"></a>Package Diagram 

- Organizes model and elements
- View system from multiple levels of abstraction
- Describes dependencies between *packages* and elements

![Package Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEnginering/images/pdiag.png "Quick Reference Guide: Package Diagram")

#### <a name="bddiag"></a>Block Definiton Diagram

- Represent structure and features of system using *blocks*
- Shows *block* properties and values
- Describes relationships between *blocks*

![Block Definition Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEnginering/images/bddiag.png "Quick Reference Guide: Block Definition Diagram")

#### <a name="ibdiag"></a>Internal Block Diagram 

- Describes internal structure of a *block*
- Contains *parts*, *ports*, and *connectors*

![Internal Block Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEnginering/images/ibdiag.png "Quick Reference Guide: Internal Block Diagram")

#### <a name="pmdiag"></a>Parametric Diagram 

- Models system constraints
- Represents a usage of constraints in an specific context
- Created within a block (internal block diagram)
- Uses equation blocks (block definition diagram)

![Parametric Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEnginering/images/pmdiag.png "Quick Reference Guide: Parametric Diagram")

### <a name="bhdiag"></a>Behaviour Diagrams 

#### <a name="ucdiag"></a>Use Case Diagram 

- Describe functionality provided by system
- Contains *actors*, *use cases*, and relationships

![Use Case Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEnginering/images/ucdiag.png "Quick Reference Guide: Use Case Diagram")

#### <a name="smdiag"></a>State Machine Diagram 

- Represents a block's life cycle, using *states* and *nodes*
- Defines system behaviour as a sequence of states a component experience in response to events
- Can be brief or detailed, as required
- Describes state enter/exit conditions (optional)

![State Machine Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEnginering/images/smdiag.png "Quick Reference Guide: State Machine Diagram")

#### <a name="atdiag"></a>Activity Diagram 

- Shows a procedural flow of system behaviour, in particular the responsibilities of each actor
- Useful for workflow modeling
- Contains *actions*, *objects*, and *nodes*
- Shows evolution of the system over time

![Activity Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEnginering/images/atdiag.png "Quick Reference Guide: Activity Diagram")

#### <a name="sqdiag"></a>Sequence Diagram 

- Decribes how a group of objects performs a process, using sequential interactions
- Shows the communication and interaction between actors
- Assigns responsibilities to blocks
- Shows evolution of the system over time

![Sequence Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEnginering/images/sqdiag.png "Quick Reference Guide: Sequence Diagram")

### <a name="rqdiag"></a>Requirements Diagram 

- Describes textual requirements contained in a specification
- Shows relationships between requirements (eg. derivation)

![Requirements Diagram](https://github.com/kathrynhamilton/textbooks/blob/master/SystemsEnginering/images/rqdiag.png "Quick Reference Guide: Requirements Diagram")

##
