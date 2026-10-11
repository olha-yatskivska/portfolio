[Back](./)

# Pairwise + EP/BVA Testing: Practical Example 

Target Application: [Pairwise Testing Web App](https://pairwise-testing.netlify.app/)       

Test Automation Repository: [Pairwise Playwright Framework](https://github.com/olha-yatskivska/pairwise-playwright-framework)   

Utility Tool: [Detailed Test Cases Generator](https://github.com/olha-yatskivska/detailed-test-cases-generator) (Custom generator used to expand combinatorial pairs into full scenario steps) 

---

## System Context & Test Strategy

**Test Environment Constraints:**

The current system under test (SUT) is a UI-only prototype. The "Your Pantry" integration is under stakeholder review regarding backend API vs internal database selection. 

**Testing Approach:**

* Single-Field Boundary Analysis: Executed prior to pairwise modeling - see [Test Matrix for Input field "Number of People"](./test-matrix.md) and [Bug reports](./bug-reports).

* Component Testing: Test Matrix for Input field "Number of People" will be automated in isolation using Playwright's component testing model (Stories and Gallery - `fixtures.mount()`) after receiving team answers to open questions (Q01-Q06).
 
* Combinatorial Reduction: Microsoft PICT was selected to build an optimal 2-wise combinatorial test suite - see [Pairwise Testing](./pairwise.md). Expected results for negative test cases will be updated once the business rules and error handling strategy (Q01-Q06) are finalized.
  
* Data-Driven Automation: High-priority test combinations were exported to a [Data-Driven CSV Dataset](./pairwise_data.csv) and executed [automatically using Pytest + Playwright](https://github.com/olha-yatskivska/pairwise-playwright-framework). 



---


See also: 

* **[Pairwise Testing](https://olha-yatskivska.github.io/pairwise.html)** - Summary of the core concepts from ISTQB Advanced Test Analyst.

* **[Pairwise Testing Tools](https://olha-yatskivska.github.io/pairwise-tools.html)** - Collection of Online, Desktop and Console Tools

* **Back to main Page**





