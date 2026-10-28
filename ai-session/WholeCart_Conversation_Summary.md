# WholeCart Functional Test Cases --- Conversation Notes

## Objective

The conversation focused on preparing and refining functional QA
test-case documentation for the WholeCart application, based on the
supplied Functional Design Document (FDD), screenshots, release notes,
and an executed test-case workbook. No application UI execution was
performed by the assistant.

## Business rules and release changes discussed

-   **BR-04 --- Minimum order:** Originally specified a minimum net
    order of ₹1,500 per seller.
-   **CR-07 --- Minimum order change:** Updated the minimum to **₹2,000
    net per seller**, overriding the original BR-04 amount.
-   **BR-07 --- Tax calculation:** Group line-item net amounts by tax
    rate, calculate tax on each rate group, and round half-up to the
    nearest paisa once per tax-rate group.
-   **BR-08 --- Delivery fee:** Apply a ₹100 delivery fee plus 18% tax
    when a seller sub-order's net value is below ₹3,000.
-   **BR-11 --- Cancellation:** Cancellation is allowed within five
    minutes, inclusive, when the order has not shipped.
-   **BR-21 --- Data access controls:** Access to data must follow the
    applicable authorization rules.
-   **CR-09 --- Invoice details:** The invoice must include supply type
    **B2B** and place of supply, including state name/code derived from
    the buyer's GSTIN.
-   **CR-11 --- Inquiry attachments:** Inquiry attachments were deferred
    to a later release.

## Test-case workbook work

### Initial workbook

An initial workbook was created with 108 functional test cases and these
sheets: - `Functional Test Cases` - `Read Me`

### Executed workbook reviewed

A later uploaded workbook was reviewed at
`WholeCart_Functional_Test_Cases(1).xlsx`. The `Functional Test Cases`
sheet contained 76 test cases, with the following status counts:

  Status         Count
  ----------- --------
  PASS              45
  FAIL              27
  Not Run            4
  **Total**     **76**

The workbook also contained these sheets: - `Bugs` - `Suggessions` -
`Observation`

The `Functional Test Cases` columns included Test Case ID, Module, User
Type, Test Case Title, Test Case Description, Preconditions, Test Steps,
Test Data, Expected Result, Actual Result, Test Case Type, Application
Environment, Status, Priority, and Bug ID.

### Major scenarios

A separate workbook was created to filter the major scenarios: - File:
`WholeCart_Major_Scenarios.xlsx` - Sheets: `Major Scenarios`,
`Summary` - It contained 69 major scenarios selected from the earlier
generated workbook.

## Clarification: minimum order per seller

The requirement is evaluated **separately for each seller**, not against
the combined cart total.

Example: - Seller A subtotal: ₹2,500 --- passes the ₹2,000 minimum. -
Seller B subtotal: ₹1,800 --- fails the ₹2,000 minimum. - Combined
subtotal: ₹4,300 --- does not make Seller B eligible.

The applicable minimum is ₹2,000 net per seller under CR-07.

## Clarification: tax rounding and paise display

Currency values should display to two decimal places. Tax should be
grouped by rate and rounded half-up once per rate group, rather than
rounding each line's tax independently.

Examples: - Two lines of ₹100.05 at 5%: grouped net ₹200.10; tax =
₹10.005, rounded half-up to **₹10.01**. - Two lines of ₹50.05 at 18%:
grouped net ₹100.10; tax = ₹18.018, rounded half-up to **₹18.02**. -
Combined net = ₹300.20; combined tax = **₹28.03**.

Use decimal arithmetic for financial calculations to avoid binary
floating-point rounding errors.

## Overall Summary workbook

The latest request was to remove the `Read Me` sheet and add an
`Overall Summary` sheet with test-case pass/fail counts and related
summary tables.

Updated file: - `WholeCart_Functional_Test_Cases_Overall_Summary.xlsx`

Changes made: - Removed the `Read Me` sheet. - Added `Overall Summary`
as the first worksheet. - Retained `Functional Test Cases`, `Bugs`,
`Suggessions`, and `Observation`. - Added a formula-linked overall
execution summary containing: - Total Test Cases - Passed - Failed - Not
Run - Blocked - Other/Blank Status - Executed (Pass + Fail) - Pass Rate
of Executed - Added a module-wise table with Total, Pass, Fail, Not Run,
and Pass Rate. - Added a priority-wise table with Total, Pass, and
Fail. - Added a bug-status summary based on the `Bugs` sheet. - Summary
formulas reference the test-case ID, module, status, and priority
columns in `Functional Test Cases`, and the status column in `Bugs`. -
The formulas are designed to update when test statuses change.

## Files referenced

  --------------------------------------------------------------------------------------------
  File                                                     Purpose
  -------------------------------------------------------- -----------------------------------
  `WholeCart_Functional_Test_Cases.xlsx`                   Initial workbook with 108
                                                           functional test cases

  `WholeCart_Major_Scenarios.xlsx`                         Workbook containing 69 major
                                                           scenarios

  `WholeCart_Functional_Test_Cases(1).xlsx`                Uploaded workbook containing
                                                           executed test results

  `WholeCart_Functional_Test_Cases_Overall_Summary.xlsx`   Updated workbook with the Overall
                                                           Summary sheet

  `WholeCart_Chat_Session.md`                              Earlier session notes file
  --------------------------------------------------------------------------------------------

## Important scope note

The assistant prepared and updated documentation and spreadsheets only.
It did not launch the WholeCart application, execute the test cases, or
independently verify application behavior.
