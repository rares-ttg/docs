Document covering all the code conventions in TTG. 
- [[#Code|Code]]
	- [[#Code#Class|Class]]
		- [[#Class#Comment|Comment]]
		- [[#Class#Naming|Naming]]
		- [[#Class#Attributes|Attributes]]
		- [[#Class#Methods|Methods]]
	- [[#Code#Package|Package]]
	- [[#Code#Module|Module]]
	- [[#Code#Library|Library]]
	- [[#Code#Micro-Service|Micro-Service]]
		- [[#Micro-Service#Naming|Naming]]
	- [[#Code#DataSource|DataSource]]
- [[#Architecture|Architecture]]
	- [[#Architecture#Constants and configurations|Constants and configurations]]
	- [[#Architecture#DTOs|DTOs]]
	- [[#Architecture#REST|REST]]
	- [[#Architecture#Class level|Class level]]
	- [[#Architecture#Module level|Module level]]
	- [[#Architecture#Service|Service]]

## Code
### Class

#### Comment
#### Naming

#### Attributes

#### Methods

### Package

- Naming... #TBD
- package-info.java must contain a description of the package's functionality, of the inputs and outputs,  and links to the corresponding documentation

### Module

- Code must be organised in modules, and module-info should contain both relevant directives (requires and export), as well as links to the relevant documentation explaining the functionality
### Library 

If code is packaged as libraries, the following rules apply: #TBD

### Micro-Service

#### Naming

### DataSource

Table names, column names, etc. #TBD

## Architecture

### Constants and configurations
### DTOs
### REST

### Class level

- Composition over inheritance
- Use interfaces
### Module level

### Service




