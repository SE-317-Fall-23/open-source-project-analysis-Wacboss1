## Project Selected: <Enter project name>

## I. Introduction
- Provide an overview of the analysis, indicating the goal of describing the types of testing used in the selected open-source project and explaining the rationale behind their choice.

## II. Types of Testing in the Project
### A. Unit Testing
- Unit testing in this project makes sure that when the project is updated, there is a lower chance of degredation.
- Since the app component is the most important component to Flask, it is heavily tested for as many conditions as possible
- Unit test in the project or executed using pytest a common python testing library.

### B. Integration Testing
- Integration testing is important in the Flask project becuase, as a backend library, the server can communicate with many different client and all transactions need to be seamless. Despite how lightweight and adaptable the Flask is.
- The main communication that is tested in flask is the interaction between a flask server and some client 
- For integration testing pytest is still used but a client object is passed in the test as well as the app object. 

### C. UI (User Interface) Testing
- As a backend library, there is no UI testing.

## III. Reasons for Choosing These Testing Types
- Discuss the rationale behind selecting these particular testing types for the project.
- Consider the project's goals, technology stack, and unique requirements when explaining the choice of testing methods.
- Highlight the benefits and advantages of using these testing types in this context.

The reason for unit testing was obvious, if this entire library is going to revolve around one component, that component must work. So by unit testing it, the can decrease the likelyhood of the App component breaking.

Integration on the other hand is less obvious. The flask library needs to be able to communicate but just checking that it puts out the right things is not enought. The communication between flask and different clients should be tested because the developer does not have any control on how the user sends their request and what structure it is in.

## 2. Test Data Generation
### A. Static Test Data
Static testing is used the most. ALl the test that check for errors or have only one input are tested statically. 

### B. Dynamic Test Data
- Explain if and how dynamic test data is used in the project.
- Provide examples of scenarios where dynamic test data is generated.

There is dynamic testing scattered throughout the test suite. The parameterized test are mainly used when a section of code can take different inputs and is suppose to change functionality accordingly. For example, the test where each type of method (get, post, put, delete, patch) is one method that has a parameter for each

## 3. Test Doubles
- Identify and explain the use of test doubles (e.g., mocks, stubs, fakes) in the project.
- Specify the specific components, functions, or cases where test doubles are applied.
- Discuss the purpose of using these test doubles in the testing strategy.

There are a lot of stubbs used throughout the test suite. When basic backend functionality needs to be tested, a stubb of the backend is created to see if it responsed the way that it should.

## 4. Discussion on Testing Practices
<!-- 
To find discussions on testing strategy in a GitHub repository, you can follow these steps:

Visit the GitHub repository for the project you're interested in.
Look for the "Issues" tab on the repository's page.
Use the search bar within the Issues tab to search for terms related to testing, such as "testing strategy," "test cases," or "test automation."
-->
- [PR](https://github.com/pallets/flask/pull/2173)
- Investigate any discussions related to testing practices within the project.
- 
- Summarize key points or insights from these discussions.
- Offer your interpretation of how the project's testing practices align with industry standards or best practices.

It would seem that at some point the examples for new users were also being tested whenever all the test were run. In the discussion, one user was thinking that they should not be run while another was thinking that running them is not a big deal. Personally, I think running those example test everytime was a waste of CICD resources, and just made testing take longer. Keeping the example code working should not come at the cost of the main code. Those test should only be ran when someone works on the example code.