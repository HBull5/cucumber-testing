# cucumber-testing

## Config your project 

* Install `cypress` && `cypress-cucumber-preprocessor` 

```command line
npm init -y 
npm i cypress
npm i cypress-cucumber-preprocessor
```

* Config cypress 
```javascript
const cucumber = require('cypress-cucumber-preprocessor').default; 

module.exports = {
  on('file:preprocessor', cucumber()); 
}
```

* Package.json will need a line right before the enclosing object
```json 
"cypress-cucumber-preprocessor": {
  "nonGlobalStepDefinitions": true
}
```

## Basics

* When creating any test you should generate at least two files. 
  * A `{feature-name}.feature` file in the `integrations` folder
  * A `{feature-name}.js` file in the `integrations` folder
  * Optionally you may want to build all of your test logic in a separate file and import it into aforementioned js file.
  
* The Feature file
  * Should include only one `Feature` This is similar to the `describe` block of a test. 
  * Should include as many `Scenario`'s as necesary, this is similar to the `it` block of a test. 
  * Should include a single or combination of `Given`, `When`, `And`, and `Then`.
  * example file: 
  ```
  Feature: Accomplishments Dashboard
    
    Scenario: should showcase error if information is missing
      Given I go to "https://localhost:3000/accomplishments" 
      When I click the Submit Accomplishment button 
      Then I see "Complete the items above to continue" 
  ```
  
* The JS file
  * Should be a directory with the same name as the feature, e.g. `Accomplishments.feature` the directory should be named `Accomplishments`, the file name is irrelevant. 
  * Should import in any of the keywords you may need to define, e.g. `Given`, `When`, `Then`
  * Should define each step, e.g. `Given`, `When`, `Then` the callback should store the code for the actual tests to be executed by cypress. 
  * You can also load in any variables you defined in your feature, check out in example above & below. 
  * example file: 
  ```javascript
  import { Given, When, Then } from 'cypress-cucumber-preprocessor/steps';
  
  Given('I go to {string}', (url) => {
    cy.visit(url);
  });
  
  When('I click the Submit Accomplishment button', () => {
    cy.contains('Submit Accomplishment').click(); 
  });
  
  Then('I see {string} error message', (text) => {
    cy.contains(text).should('be.visible');
  });
  ```
  
## Running Tests 

* Open cypress `npx cypress open` 
* Run the `feature` file you desire. 
