blue-red-testing
==========
A/B testing made easy. (modified version of [ab-testing](https://www.npmjs.com/package/ab-testing) package by [@xavimb](https://github.com/xavimb))

## Install

	npm install ab-testing

## Initialize

```
var ABTesting = require('ab-testing');

var testObject = ABTesting.createTest('firstTest', 	// This name has to be unique across all the tests
[
	{
		name: 'A',
		weight: 0.1 	// If not set, the default value is 0.5
		outcome: true // The value returned if the user is in this bucket (can be anything)
	},
	{
		name: 'B',
		weight: 0.9
		outcome: false
	}
]);
```

## Assign a group

```
// Given a unique ID of the user, returns 'A' or 'B'
var testGroup = testObject.getGroup(user.id);
```

## Get test name

```
// Returns the name of the test, in this case 'firstTest'
var testName = testObject.getName();
```

## A/B Test

```
// Executes the test and returns the outcome for the given user
testObject.test(testGroup, this);
```

## Useful usage tips

```
// Use the test name and the group name to track analytics
sendToAnalytics(testName, testGroup);
```

## Create multiple A/B tests

```
var ABTesting = require('ab-testing');

var landingPageTest = ABTesting.createTest('landingPage', [{ name: 'oldLandingPage' }, { name: 'newLandingPage' }]);
var pricingPageTest = ABTesting.createTest('pricingPage', [{ name: 'oldPricingPage' }, { name: 'newPricingPage' }]);

...

var landingPageGroup = pandingPageTest.getGroup(req.account.username);
var pricingPageGroup = pricingPageTest.getGroup(req.account.username);

...

landingPageTest.test(landingPageGroup, [
	function () {
		// oldLandingPage code
	},
	function () {
		// newLandingPage code
	}
], this);

pricingPageTest.test(pricingPageGroup, [
	function () {
		// oldPricingPage code
	},
	function () {
		// newPricingPage code
	}
], this);
```

>NB: the last parameter `this` is optional. If the scope is not required, this paremeter can be ignored.

