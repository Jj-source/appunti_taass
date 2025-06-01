2025-03-03 18:42

Status: #baby

Tags: [[Project & People Management]] [[GRASP patterns]] [[GOF patterns]]
# Object Oriented Analysis (OOA)

**Scopo: modularità e info hiding**.
Invece di affrontare il problema con flow diagrams, la OO analysis usa ‘use cases’ e ‘user stories’ 
#### OOA model
- Set of key classes with detailed information about their data structure and operations
- Evolves into OOD model
- OOA model only deals with objects of the problem domain and their features: Not the language-specific features or detailed data structures
- Must be totally independent from user interface and database
- UML Class Diagram: OOA model
#### Come identifichi oggetti e classi?
- We look at the use cases / user stories
	- We extract the nouns and the verbs
	- Nouns help identifying objects
	- Verbs help identifying methods
- We pose particular attention at:
	- Avoiding using the same term for different entities
	- Avoiding to use different terms for the same entity
	  
![[OOAcategorie.png]]

### CRC method
C: Class
	Finds the classes of objects constituting the system
R: Responsibility
	Defines responsibility of the classes
C: Collaboration
	Finds collaborations (exchange of info) needed among classes to fulfill the responsibilities
Distinction to be made:
- Classes for OOA
- Objects for working systems
#### CRC Cards

| Class Name          |               |
| ------------------- | ------------- |
| Main Responsibility |               |
| Responsibilities    | Collaborators |
| ...                 | ...           |
#### Brainstorming
1. Identify candidate classes
2. Choose a coherent set of use case, scenarios, user stories
3. Walk through the scenario, naming cards and responsibilities
4. Vary the situations to stress test the cards
5. Add cards, push cards to the side to let the design evolve

![[OOAex.png]]