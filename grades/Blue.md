# Principles
## Design and Implementation do not overlap
 Violates the DRY principe. 
 When they overlap the design documents will not match to the implementation and this will do more harm. 
 So try to make the design not overlaping with the implementation. In Microservice world this is seprated by
 Macro and Micro Architecture.
 
 ### Example
 A GUI design could specify Events and MVP usage but it did not specify the frameworks or methods used it just tells you how they communicate and which abstractions are used.

## Implementation reflects Design
There is no need for a design document when the implementation does something else. The architecture ensures the implementation is simple.

## You Ain't Gonna Need It (YAGNI)
Only implement things you need now. 
Do not implement things you can maybe use some day in the future. Do the simplest thing that could possibly work.

# Practices
## Continuous Delivery
Next step after Continuous Integration. 
This ensures the whole release process is tested and automatically performed for each changeset. 
So its possible to release faster and more frequently.

## Iterative Development
Its impossible to produce a good functional product with upfront planning and only one release. 
To be able to adjust the course to new influences like customer wishes, market changes it is needed to do iterative development. 

## Components
With Black-Box modules it is possible to program parallel and its easier to extend the software because the components are decoupled from each other.

## Test first
So the tests become the specification of the software and always check if the software does what the customer wants. 
