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

Check if at least one of the elements referenced by the valid `aria-describedby` attribute values exists.

if yes, continue with [step 2](#step-2)

else, return

| Outcome  | Failed
|----------|-----
| ID       | SC1-1-1-aria-describedby-fail1
| Error    | None of the elements referenced by aria-describedby exists.


### Step 2
Test method: [manual][earl:manual]

...


[earl:automatic]: pages/test-modes.md#automatic
[earl:semiauto]: pages/test-modes.md#automatic
[earl:manual]:  pages/test-modes.md#manual