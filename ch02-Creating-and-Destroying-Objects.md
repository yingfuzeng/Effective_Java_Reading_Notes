# Creating and Destroying Objects
### Syntactic stuff I learned along the way
**Static Fields:**
If a field is declared *static*, there exists exactly one incarnation of the field, no matter how many instances of the class may eventually be created.
##Item 1: Consider static factory methods instead of constructors
**Pros**
	1. We can name the factory methods, making the code easier to read.  As opposed to modify the signitures of 
	constructors (e.g. different parameter types).
	2. 