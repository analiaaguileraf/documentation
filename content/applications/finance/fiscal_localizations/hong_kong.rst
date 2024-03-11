=========
Hong Kong
=========

Configuration
=============

First, install the 🇭🇰 `Hong Kong - Accounting` fiscal localization module to get the latest features of HK Localization.

.. image:: hong_kong/l10n-hk-modules.png
   :alt: Hong Kong localization modules

.. note::
   To use the *Payroll* features, install the module under the :ref:`HK Payroll <hong_kong/payroll>`.

Add FPS QR codes to invoices
============================

:abbr:`FPS (Faster Payment System)` is a payment service platform that allows customers to make
instant domestic payments to individuals and merchants in Hong Kong dollars or Renminbi via online
and mobile banking.

Activate QR codes
-----------------

Go to :menuselection:`Accounting app --> Configuration --> Settings`. Under the :guilabel:`Customer
Payments` section, activate the :guilabel:`QR Codes` feature.

FPS bank account configuration
------------------------------

Go to :menuselection:`Contacts app --> Configuration --> Bank Accounts: Bank Accounts` and select the bank account for
FPS activation. Set the :guilabel:`Proxy Type` and fill in the :guilabel:`Proxy Value` field depending
on the type chosen.

.. important::
   - The account holder's country must be set to Hong Kong on its contact form.
   - Remember to include the invoice number in the QR code by checking the :guilabel:`Include Reference` checkbox.

.. image:: hong_kong/hk-fps-bank-setting.png
   :alt: FPS bank account configuration

.. seealso::
   :doc:`../accounting/bank`

Bank journal configuration
--------------------------

Go to :menuselection:`Accounting app --> Configuration --> Journals`, open the bank journal, then fill
out the :guilabel:`Account Number` and :guilabel:`Bank` under the :guilabel:`Journal Entries` tab.

.. image:: hong_kong/hk-bank-account-journal-setting.png
   :alt: Bank Account's journal configuration

Issue invoices with FPS QR codes
--------------------------------

When creating a new invoice, open the :guilabel:`Other Info` tab and set the :guilabel:`Payment
QR-code` option to *EMV Merchant-Presented QR-code*.

.. image:: hong_kong/hk-qr-code-invoice-setting.png
   :alt: Select EMV Merchant-Presented QR-code option

Ensure that the :guilabel:`Recipient Bank` is configured, as Odoo uses this field to generate the FPS QR code.

.. _hong_kong/payroll:

Payroll
=======

.. important::
   Ensure the 🇭🇰 `Hong Kong - Payroll` module is installed before proceeding.

.. image:: hong_kong/hk-payroll-module.png
   :alt: HK Payroll module

Create employees
----------------

Go to the *Employees* app and click :guilabel:`New`.

Here are a list of supplementary fields to input before starting:

Under the :guilabel:`Work Information` tab:

- :guilabel:`Working Hours`: HK Standard 40 hours/week **must** be selected.

Under the :guilabel:`Private Information` tab:

- :guilabel:`Surname, Given Name, Name in Chinese`: Name of the employee
- :guilabel:`Identification No`: HKID of the employee
- :guilabel:`Gender`: Gender of the employee
- :guilabel:`Private Address`: Address of the employee
- :guilabel:`Bank Account Number`: Employee's bank account number
- :guilabel:`Current Rental`: Employee's rental records (if rental allowance is applicable)
- :guilabel:`Autopay Type`: BBAN, SVID, EMAL, etc
- :guilabel:`Autopay Reference`: Autopay Reference Number

.. important::
   For the :guilabel:`Bank Account Number`, set the :guilabel:`Send Money` field to :guilabel:`Trusted`. If
   this is not set to :guilabel:`Trusted`, money **cannot** be tranferred to the employee's bank acocunt.

.. note::
   For the :guilabel:`Current Rental`, set the Current Rental's :guilabel:`state` to :guilabel:`Running`.

Under the :guilabel:`HR Settings` tab:

- :guilabel:`Volunteer Contribution Option`: Select either :abbr:`MC (Mandatory Contribution)`, Fixed % :abbr:`VC (Voluntary Contribution)` or Cap 5% VC (max-out at 5%), if desired.
- :guilabel:`MPF Manulife Account`: Account number if applicable.

Manage contracts
----------------

Once the new employee has been created, click the :guilabel:`Contracts` smart button on the
employee record, or navigate to :menuselection:`Employees app--> Employees --> Contracts`.

.. note::
   Only **one** contract can be active simultaneously per employee, but an employee can be assigned
   consecutive contracts during their employment.

The following are critical for setting up a contract:

- :guilabel:`Working Schedule`: Set as HK Standard 40 hours/week (from employee record)
- :guilabel:`Salary Structue Type`: Set as CAP57: Hong Kong Employee.
- :guilabel:`Work Entry Source`: Select either :guilabel:`Working Schedule`, :guilabel:`Attendances` or :guilabel:`Planning`.
  This field determines how the work entries are accounted for in the payslip.

   - :guilabel:`Working Schedule`: The work entries are generated automatically based on the employee's working schedule.
   - :guilabel:`Attendances`: The work entries are generated based on the check-in/-out period logged in the *Attendances* app.
   - :guilabel:`Planning`: The work entries are generated from planning shifts only.

Under the :guilabel:`Salary Information` tab:

- :guilabel:`Wage Type`: Select :guilabel:`Fixed Wage` for Full-time or Part-time employees, or :guilabel:`Hourly Wage` for employees who are paid hourly.
- :guilabel:`Wage`: Monthly or Hourly depending on the company.
- :guilabel:`Internet Subscription`: This is an **optional** field to provide additional internet allowance on top of the current salary package.

  .. important::
     Timesheets do **not** impact work entries in Odoo.

Once all information has been setup, set the contract status to :guilabel:`Running` by clicking the :guilabel:`Running` button
in the top-right of the page.

.. image:: hong_kong/hk-contract.png
   :alt: Hong Kong employment contract

.. _hong_kong/running_payslips:

Generate payslips
-----------------

Once the employees and their contracts are configured, payslips can be generated in the *Payroll* app.

Odoo provides **four** different salary structures under CAP57 Regulation:

#. :guilabel:`Employees Monthly Pay`: To process the monthly employee salary.
#. :guilabel:`Payment in Lieu of Notice`: To process final payment upon contract termination.
#. :guilabel:`Long Service Payment`: Applicable to employees with more than five years of service upon
   contract termination.
#. :guilabel:`Severance Payment`: Applicable to employees with more than two years of service upon
   contract termination.

Before running the payslips, the accounts used in the salary rule can be adjusted by navigating to
:menuselection:`Payroll app --> Configurations --> Rules`.

.. image:: hong_kong/hk-salary-rules.png
   :alt: Hong Kong Salary Rules

Odoo can create pay runs in **two** ways: via **batch** or **individual** payslips.

.. _hong_kong/batch_payslips:

Batch payslips
~~~~~~~~~~~~~~

Go to :menuselection:`Payroll app --> Payslips --> Batches`.
This method of payslip generation is used for recurring payments, since multiple employee payslips
can be managed at once.

#. Click on :guilabel:`New`.
#. Enter a :guilabel:`Batch Name` (e.g, `2024 – Jan`) and :guilabel:`Period` (e.g. 01/01/2024 - 01/31/2024).
#. Click on :guilabel:`Generate Payslips`.
#. Choose which :guilabel:`Salary Structure` to use for this batch. The department filter allows the batch to
   apply to only a specific group of employees.
#. Click on :guilabel:`Generate`.
#. A :guilabel:`Payslips` smart button is created automatically.

.. image:: hong_kong/hk-batch-payslips.png
   :alt: Hong Kong Batch Payslips

Next, click :guilabel:`Create Draft Entry` to generate a draft journal entry found in the :guilabel:`Other Info`
tab of each payslips. A :guilabel:`Confirmation` pop-up window appears asking `Are you sure you want to proceed?`.
Click :guilabel:`Ok` to create the journal entries.

Individual payslips
~~~~~~~~~~~~~~~~~~~

Go to :menuselection:`Payroll app --> Payslips --> All Payslips`
This method of payslip generation is commonly used to handle non-recurring payments (e.g. Payment in Lieu
of Notice, Long Service Payment, Severance Payment).

#. Click on :guilabel:`New`.
#. Select an :guilabel:`Employee`; their :guilabel:`Contract` are filled out automatically.
#. Add a pay :guilabel:`Period`.
#. Select a salary :guilabel:`Structure` (e.g. Employees Monthly Pay)
#. The :guilabel:`Worked Days` tab automatically compute the worked days/hours and time off leaves
   that are applicable.
#. Additional payslip items can be added at this time (e.g. Commissions, Deductions) under the
   :guilabel:`Other Inputs` section.
#. Click on :guilabel:`Compute Sheet` button to generate the payslip lines. This button updates
   the :guilabel:`Salary Computation` tab.

.. image:: hong_kong/hk-individual-payslip.png
   :alt: Hong Kong Individual Payslip

.. note::
   If the work entry for an employee was amended, click the :guilabel:` ⚙ (gear)` icon, then click
   :guilabel:`Recompute Whole Sheet` to refresh the payslip's :guilabel:`Worked Days & Inputs` section.

The :guilabel:`Salary Computation` tab shows the detailed breakdown of the computation based on
the salary rules configured for each structure type.

.. image:: hong_kong/hk-salary-computation.png
   :alt: Hong Kong Salary computation

#. :guilabel:`Rent Allowance`: Amount derived from the employee's active rental record.
#. :guilabel:`Basic Salary`: Amount of base salary provided (after rent allowance deduction)
#. :guilabel:`713 Gross`: Net payable amount considering Commission, Internet Allowance, Reimbursements,
   Back-pay, Deduction, etc.
#. :guilabel:`MPF Gross`: Net payable amount from 713 gross after consideration of additional allowances,
   deductions and end-of-year payment.
#. :guilabel:`Employee Mandatory Contribution`: Employee MPF Contribution
#. :guilabel:`Employer Mandatory Contribution`: Employer MPF Contribution
#. :guilabel:`Gross`: Net payable amount from MPF gross after consideration of MPF deductions.
#. :guilabel:`Net Salary`: Final payable amount to be paid to the employee.

.. important::
   There are no MPF contributions for the first month. Both **employee** and **employer**
   contribution starts on **second** month.

Under the :guilabel:`Other Inputs` tab at the bottom of payslip, there are additional manual input
types that are specific to *HK Payroll*:

- :guilabel:`Back Pay`: Additional salary payout can be included under this category.
- :guilabel:`Commission`: The commission earned during the period can be manually entered here.
- :guilabel:`Global Deduction`: A lump-sum deduction from the entire payslip.
- :guilabel:`Global Reimbursement`: A lump-sum reimbursement to the entire payslip.
- :guilabel:`Referral Fee`: The additional bonus offered for any form of business-related referral.
- :guilabel:`Moving Daily Wage`: To override the :abbr:`ADW (Average Daily Wage)` value used for leaves computation.
- :guilabel:`Skip Rent Allowance`: If set, the rental allowance is excluded from the current payslip.
- :guilabel:`Custom Average Monthly Salary`: To override the average monthly salary used for end-of-year payment.

Once the payslips are ready, click :guilabel:`Create Draft entry` to generate a draft journal entry
found in the :guilabel:`Other Info` tab of the payslip.

Paying employees
----------------

Once the draft journal entries have been posted, the company can now pay the employees.
The user can choose between **two** different **payment methods**.

- From the employee's payslip (:menuselection:`Payroll app --> Payslips --> All Payslips`), once the payslip's journal
  entry has been posted, click :guilabel:`Register Payment`. The process is the same as
  :doc:`paying vendor bills <../accounting/payments>`. Select the desired bank journal and payment
  method, then later reconcile the payment with the corresponding bank statement.

- For batch payments, once all draft journal entries from the batch are confirmed, click :guilabel:`Mark as Paid`
  to post the payment journal entry. Then create a :doc:`payment <../accounting/payments>` in the *Accounting*
  app and reconcile accordingly.

Attendances & Hourly Wage
-------------------------

Setup the contract as follows for employees who are based paid on an hourly-wage contract:

.. important::
   Make sure the employee contract is using *Attendances* as the Work Entry Source and the Wage
   Type is set to :guilabel:`Hourly Wage`.

#. Go to *Attendance* app.
#. The employee can check-in/out via the kiosk mode.
#. In the *Payroll* app, review the attendance work entries generated from
   :menuselection:`Payroll app --> Work Entries --> Work Entries`.
#. Next, generate the :ref:`payslips <hong_kong/running_payslips>` and process the payment.

.. image:: hong_kong/hk-attendance-work-entry.png
   :alt: Hong Kong Attendance Work Entry

.. image:: hong_kong/hk-attendance-payslip.png
   :alt: Hong Kong Attendance Payslip

Time Off with Payroll
---------------------

The work entry types and time off types are fully integrated between the *Time Off* and
*Payroll* apps. There are several time off types and work entry types specific to Hong Kong which are
installed automatically along with the *HK Payroll* module.

There are two checkboxes to be considered when setting up the work entry type:

- :guilabel:`Use 713`: This leave type to be included as part of 713 computation.
- :guilabel:`Non-full pay`: 80% of the :abbr:`ADW (Average Daily Wage)`.

.. image:: hong_kong/hk-work-entry-type.png
   :alt: Hong Kong Work Entry Type

Understanding 713 Ordinance
---------------------------

The *HK Payroll* module is compliant with 713 Ordinance which relates to the
:abbr:`ADW (Average Daily Wage)` computation to ensure fair compensation for employees.

The ADW computation is as follows:

.. image:: hong_kong/hk-adw.png
   :alt: Hong Kong ADW Formula

.. note::
   For 418 compliance, there is no automated allocation of the **Statutory Holiday**
   entitlement to the employees. As soon as 418 requirements are met, manually allocate the leaves
   via the *Time Off* app.

.. note::
   Before generating payslips, ensure the statuses are :guilabel:`Done`
   to validate the outcome:

.. list-table::
   :header-rows: 1

   * - Period
     - Days
     - Wage
     - Commission
     - Total
     - ADW
     - Leave Value
   * - Jan
     - 31
     - $20200
     - $0
     - $20200
     - $651.61 ($20200/31)
     - N/A
   * - Feb
     - 28
     - $20200
     - $5000
     - $25200
     - $769.49 ($45400/59)
     - N/A
   * - Mar (One Day Annual Leave)
     - 31
     - $20324.33
     - $0
     - $20324.33
     - $730.27 ($65724.33/90)
     - $769.49
   * - Apr (One Day 80% Sick Leave)
     - 30
     - $20117.56
     - $0
     - -
     - -
     - $584.22 ($730.27*0.8)

Here is an example demonstrating the 713 logic:

- :guilabel:`Jan`: Generate a payslip with a monthly wage of $20200. The :abbr:`ADW (Average Daily Wage)` is always computed on a cumulative basis of the trailing 12-months.
- :guilabel:`Feb`: Generate a similar payslip but add an :guilabel:`Other Input Type` for the Commission.
- :guilabel:`Mar`: Apply for **one** full-paid annual leave in March. The salary compensation for the leave taken is based on :abbr:`ADW (Average Daily Wage)` thus far.

.. image:: hong_kong/hk-march-713.png
   :alt: Hong Kong March 713

- :guilabel:`Apr`: Apply for a 1-day non-full pay leave in April. Since this is a non-full pay leave, the :abbr:`ADW (Average Daily Wage)` is computed accordingly.

.. image:: hong_kong/hk-apr-713.png
   :alt: Hong Kong April 713

.. note::
   The value of :abbr:`ADW (Average Daily Wage)` is computed in the backend and not be visible to the user.

.. seealso::
   - `HK 713 Ordinance <https://www.labour.gov.hk/eng/public/wcp/ConciseGuide/Appendix1.pdf>`_
   - `HK 418 Ordinance <https://www.workstem.com/hk/en/blog/418-regulations/>`_

Generate reports
----------------

Before generating the below reports, setup the following in
:menuselection:`Settings app --> Payroll --> Accounting/HK Localization`.

.. image:: hong_kong/hk-report-setup.png
   :alt: Hong Kong Payroll Settings

IRD Report
~~~~~~~~~~

There are a total of **four** IRD reports available:

- :guilabel:`IR56B`: Employer's Return of Remuneration and Pensions
- :guilabel:`IR56E`: Notification of Commencement of Employment
- :guilabel:`IR56F`: Notification of Ceasation of Employment (remaining in HK)
- :guilabel:`IR56G`: Notification of Ceasation of Employment (departing from HK permanently)

Go to :menuselection:`Payroll app --> Reporting --> IR56B/E/F/G`:

#. Click on :guilabel:`New`.
#. Fill in the relevant information for the IRD report.
#. Click on :guilabel:`Populate` and the :guilabel:`Eligible Employees` smart button appears.
#. The :guilabel:`Employee Declarations` status is :guilabel:`Draft` and changed to :guilabel:`Generated PDF` status
   once the schedule runs.
#. Once the PDF is generated, the IRD form may be downloaded.

.. image:: hong_kong/hk-ir56b.png
   :alt: Hong Kong IR56B report

.. note::
   The scheduled action called :guilabel:`Payroll:Generate pdfs` can be manually triggered.
   It is set by default to run the PDF generation monthly.

Manulife MPF Sheet
~~~~~~~~~~~~~~~~~~

Go to :menuselection:`Payroll app --> Reporting --> Manulife MPF Sheet`.

#. Click on :guilabel:`New`.
#. Select the relevant Year, Month and Sequence No.
#. Click on :guilabel:`Create XLSX`.
#. The Manulife MPF XLSX file is then generated and available for download.

.. image:: hong_kong/hk-manulife-sheet.png
   :alt: Hong Kong Manulife Sheet

.. note::
   Odoo will not be developing further reports for other MPF trustee as there is soon an
   e-MPF platform setup by the local government.

.. seealso::
   - `eMPF <https://www.mpfa.org.hk/en/empf/overview>`_

HSBC Autopay Report
~~~~~~~~~~~~~~~~~~~

If :guilabel:`HSBC Autopay` is selected as the batch payment method, click on :guilabel:`Craete HSBC Autopay Report`.
and fill in the mandatory fields:

.. image:: hong_kong/hk-generate-autopay.png
   :alt: Hong Kong HSBC Autopay Wizard

This creates an **.apc** file format which can be uploaded to the HSCB portal for processing.
