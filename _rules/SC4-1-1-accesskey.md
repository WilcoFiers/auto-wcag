---
rule_id: SC4-1-1-accesskey
name: Provide unique accesskeys
test_mode: automatic

criteria:
- 4.1.1 # Parsing (Level A)

author:

---

## Description

This test checks accesskey attribute for all elements to have a unique value.

## Background

- [F17: Failure of Success Criterion 1.3.1 and 4.1.1 due to insufficient information in DOM to determine one-to-one relationships (e.g., between labels with same id) in HTML](http://www.w3.org/TR/2014/NOTE-WCAG20-TECHS-20140311/F17)
- [eGovMon test F17-1](http://wiki.egovmon.no/wiki/SC4.1.1#ID:_F17-1)

## Assumptions

- If the accesskey value has multiple characters the user agent picks the first character and ignores the rest. See: [WHATWG on Interaction](http://www.whatwg.org/specs/web-apps/current-work/multipage/interaction.html#the-accesskey-attribute).

## Test properties

| Property          | Value
|-------------------|----
| Test name         | Provide unique accesskeys
| Test requirement  | 4.1.1 Parsing
| Test mode         | Automatic
| Test environment  | DOM
| Test subject      | single web page

## Test procedure

### Selector

Test mode: [automatic][AUTO]

Select any element with an accesskey attribute. The following CSS selector could be used: *[accesskey]

### Step 1

Test mode: [automatic][AUTO]

- IF there is no list called 'knownAccesskeys':
  -  Create an empty list 'knownAccesskeys;
- Take the first character of the ACCESSKEY attribute as FirstChar
- IF the FirstChar exists in 'knownAccesskeys':
  - Return {{ page.rule_id }}-fail1
- ELSE:
  - Add the FirstChar to 'knownAccesskeys'
  - Return {{ page.rule_id }}-pass1

| Outcome  | Passed
|----------|-----
| Testcase | {{ page.rule_id }}
| Pointer  | selector result
| ID       | {{ page.rule_id }}-pass1

| Outcome  | Failed
|----------|-----
| Testcase | {{ page.rule_id }}
| Error    | The accesskey of this element has occurred before on this page
| Pointer  | selector result
| ID       | {{ page.rule_id }}-fail1

[AUTO]: ../pages/test-modes.html#automatic
[MANUAL]: ../pages/test-modes.html#manual