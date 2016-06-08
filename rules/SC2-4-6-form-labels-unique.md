# SC2-4-6-form-labels-unique

## Description
The goal of this rule is to test that names given to input elements are unique, within their particular context.


## Background
- [G131: Providing descriptive labels](https://www.w3.org/TR/WCAG20-TECHS/G131.html)


## Assumptions
- Forms do not require information to be entered twice for the same reason. For example, a password field may require verification, but if this field was given the same label, this would be an accessibility violation. Similarly, if a form has two 'date' fields, these are assumed to have a different purpose, such as start date and end date, and so the labels of both are not descriptive
- The association between form field and label is assumed to be correct. If two form fields refer to the same label, one correctly, and one incorrectly, this could be a violation of 1.3.1 instead of 2.4.6. As both types of violations would prevent meeting level AA conformance, this inaccuracy is permitted.
- Similarly it is assumed the programatically determinable label is not significantly different from the visible label. This could be a different element. If these are very different (which should be considered a WCAG violation on it's own) this rule will not return accurate results.

*Note:* This rule is dependent on the presence of programatically determinable labels, which is tested for in success criterion [1.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html) and [4.1.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/ensure-compat-rsv.html).


## Test properties
| Properties        | Values
|-------------------|-----------
| Test name         | Form fields are unique in their context
| Success criterion | [2.4.6 Headings and Labels](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-descriptive.html)
| Test mode         | automated
| Test environment  | DOM
| Test Subject      | Single page


## Test procedure


### Selector
Test method: [automatic][earl:automatic]

Select every element with one of the following roles: `checkbox`, `combobox`, `listbox`, `searchbox`, `slider`, `switch`, `textbox`.

These elements can be found using the following CSS selector:
```
*[role=checkbox], *[role=combobox], *[role=listbox], *[role=searchbox], *[role=slider], *[role=switch], *[role=textbox], input:not([type=hidden]):not([type=button]):not([type=submit]):not([type=reset]):not([type=image]):not([role]), textarea:not([role]), select:note([role])
```

### Step 1
Test method: [automatic][earl:automatic]

Find the closest ancestor of the selected form field, that is either a fieldset, form element, has the role of radiogroup (in case the selected element is a radiobutton), or the root of the document. This element is the *context element*.

Compute the *accessible name* of the seleected form field, using the [name computation algorithm](name-compute)

Take each element from the *context element*, that matches the selector of this rule, excluding the currently selected element. Put these in a list of *other form fields*.

For each element in the *other form fields* list, compute the accesslbie name and compare it to that of the selected element. Put each element with the same accessible name in a list *same name fields*.

Check if the *same name fields* list has any elements in it.

If yes, continue with [step 2](#step-2)

If no, return:

| Outcome  | Passed
|----------|-----
| ID       | SC2-4-6-form-labels-unique


### Step 2

... compare descriptions

## Open questions

- Is this always true in the case of radiobuttons and select elements?
- Should the 'type' of input be considered? Example: allow mobile phone to be used for a checkbox and a text field in the same form?
- Does this rule correctly interpret things like phone number fields broken up into two input fields?

[earl:automatic]: pages/test-modes.md#automatic
[earl:semiauto]: pages/test-modes.md#automatic
[earl:manual]:  pages/test-modes.md#manual
[name-compute]: ...
