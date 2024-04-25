==================
AvaTax integration
==================

Avalara's *AvaTax* is a cloud-based tax software. Integrating AvaTax with Odoo provides real-time
and region-specific tax calculations when users sell, purchase, and invoice items in Odoo. *AvaTax*
tax calculation is supported with every United Nations charted country, including inter-border
transactions.

.. important::
   AvaTax is only available for integration with databases/companies that have locations in the
   United States and Canada.

*AvaTax* accounts for location-based tax rates for each state, county and city. It improves
remittance accuracy by paying close attention to laws, rules, jurisdiction boundaries, and special
circumstances like tax holidays and product exemptions. Companies who integrate with *AvaTax* can
maintain control of tax-calculations in-house with this simple :abbr:`API (application programming
interface)` integration.

Avalara provides the following services:

- AvaTax (sales and use tax calculations)
- Avalara returns (prepare, file, and remit sales tax returns)
- Avalara Exemption Certificate Management (collect, store, and manage documents)
- Avalara tax Research (Get tax research in plain language)
- Avalara Business License Services (project based assistance to help confront challenges to their
  license operations)

.. important::
   Some limitations exist in Odoo while using AvaTax for tax calculation:

   - AvaTax is not supported in Odoo *Point of Sale*, because a dynamic tax calculation model is
     excessive for transactions within a single delivery address, such as stores or restaurants.

   - AvaTax and Odoo use the company address and not the warehouse address.

   - Exercise tax is not supported. This includes tabacco/vape taxes, fuel taxes, and other specific
     industries.

.. seealso::
   Avalara's support documents: `About AvaTax
   <https://community.avalara.com/support/s/document-item?language=en_US&bundleId=dqa1657870670369_dqa1657870670369&topicId=About_AvaTax.html&_LANG=enus>`_

Set up on AvaTax (onboarding)
=============================

To use *AvaTax*, an account with Avalara is required for the setup. If one has not been set up yet,
connect with Avalara to purchase a license: `Avalara: Let's Talk
<https://www.avalara.com/us/en/get-started.html>`_.

.. tip::
   Upon account setup, take note of the AvaTax :guilabel:`Account ID`. This will be needed in the
   :ref:`Odoo setup <avatax/credentials>`. In Odoo this number is the :guilabel:`API ID`.

Then, `create a basic company profile
<https://community.avalara.com/support/s/document-item?bundleId=dqa1657870670369_dqa1657870670369&topicId=Create_a_Basic_company_profile.html&_LANG=enus>`_.

Create basic company profile
----------------------------

Collect essential business details for the next step: locations where tax is collected,
products/services sold and their sales locations, and customer tax exemptions, if applicable. Follow
the Avalara documentation for creating a basic company profile:

#. `Add your company information
   <https://community.avalara.com/support/s/document-item?bundleId=dqa1657870670369_dqa1657870670369&topicId=Add_your_company_information.html&_LANG=enus>`_.
#. `Tell us where you collect and pay tax
   <https://community.avalara.com/support/s/document-item?bundleId=dqa1657870670369_dqa1657870670369&topicId=Tell_us_where_you_collect_and_pay_tax.html&_LANG=enus>`_.
#. `Verify your jurisdictions and activate your company
   <https://community.avalara.com/support/s/document-item?bundleId=dqa1657870670369_dqa1657870670369&topicId=Verify_your_jurisdictions_and_activate_your_company.html&_LANG=enus>`_.
#. `Add other company locations for location-based filing
   <https://community.avalara.com/support/s/document-item?bundleId=dqa1657870670369_dqa1657870670369&topicId=Add_other_company_locations_for_location-based_filing.html&_LANG=enus>`_.
#. `Add a marketplace to your company profile
   <https://community.avalara.com/support/s/document-item?bundleId=dqa1657870670369_dqa1657870670369&topicId=Add_marketplace_transactions_to_your_company_profile.html&_LANG=enus>`_.

.. _avatax/create_avalara_credentials:

Connect to AvaTax
=================

After creating the basic company profile in Avalara, connect to AvaTax. This step links Odoo and
AvaTax bidirectionally.

Navigate to either Avalara's `sandbox <https://sandbox.admin.avalara.com/>`_ or `production
<https://admin.avalara.com/>`_ environment. This will depend on which type of Avalara account the
company would like to integrate.

.. seealso::
   `Sandbox vs production environments in Avalara
   <https://knowledge.avalara.com/bundle/fzc1692293626742/page/sandbox-vs-production.html>`_.

Log in to create the :guilabel:`License Key`. Go to :menuselection:`Settings --> License and API
Keys`. Click :guilabel:`Generate License Key`.

.. note::
   A warning will display stating: `If your business app is connected to Avalara solutions, the
   connection will be broken until you update the app with the new license key. This action cannot
   be undone.`

   Generating a new license key breaks the connection with existing business apps using the *AvaTax*
   integration. Ensure to update these apps with the new license key.

Should this be the first :abbr:`API (application programming interface)` integration being made with
AvaTax and Odoo, then click :guilabel:`Generate license key`.

Should this be an additional license key then, ensure the previous connection can be broken. There
is **only** one license key associated with each of the Avalara sandbox and production accounts.

Copy this key to a safe place. It is **strongly encouraged** to backup the license key for future
reference. This key cannot be retrieved after leaving this screen.

Configuration in Odoo
=====================

Before using AvaTax there are some additional configurations in Odoo to ensure tax calculations are
made accurately.

Verify that the Odoo database contains necessary data. The country initially set up in the database
determines the fiscal position and aids AvaTax in calculating accurate tax rates.

Fiscal country
--------------

To set the :guilabel:`Fiscal Country`, navigate to :menuselection:`Accounting app --> Configuration
--> Settings`.

.. seealso::
   :doc:`../../fiscal_localizations`

Under the :guilabel:`Taxes` section, set the :guilabel:`Fiscal Country` feature to :guilabel:`United
States` or :guilabel:`Canada`.

Company settings
----------------

All companies operating under the Odoo database should have a full and complete address listed in
the settings. Navigate to :menuselection:`Settings app`, and under the :guilabel:`Companies`
section, ensure there is only one company operating the Odoo database. Click :guilabel:`Update Info`
to open a separate page to update company details.

Should there be multiple companies operating in the database, click :guilabel:`Manage Companies` to
load a list of companies to select from. Update company information by clicking into the specific
company.

Database administrators should ensure that the :guilabel:`Street...`, :guilabel:`Street2...`,
:guilabel:`City`, :guilabel:`State`, :guilabel:`ZIP`, and :guilabel:`Country` are all updated for
the companies.

This will ensure accurate tax calculations and smooth end-of-year accounting operations.

.. seealso::
   - :doc:`../../../general/companies`
   - :doc:`../get_started`

Module installation
-------------------

Next, ensure that the Odoo *AvaTax* module is installed. To do so, navigate to :menuselection:`Apps
application`. In the :guilabel:`Search...` bar, type in `avatax`. Press enter and the following
results populate:

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Name
     - Technical name
     - Description
   * - :guilabel:`Avatax`
     - `account_avatax`
     - Default *AvaTax* module. This module adds the base *AvaTax* features for tax calculation.
   * - :guilabel:`Avatax for SO`
     - `account_avatax_sale`
     - Includes the information needed for tax calculation on sales orders in Odoo.
   * - :guilabel:`Avatax for Subscriptions`
     - `account_avatax_sale_subscription`
     - This module includes the features required for tax calculation on subscriptions in Odoo.
   * - :guilabel:`Avatax Brazil`
     - `l10n_br_avatax`
     - Includes information for tax calculation in the Brazil localization.
   * - :guilabel:`Avatax for SOs in Brazil`
     - `l10n_br_avatax_sale`
     - This module includes the features required for tax calculation for sales orders in the Brazil
       localization.
   * - :guilabel:`Account Avatax - Ecommerce`
     - `website_sale_account_avatax`
     - Includes tax calculation features for the checkout process on Odoo eCommerce.
   * - :guilabel:`Account AvaTax - Ecommerce - Delivery`
     - `website_sale_delivery_avatax`
     - Includes tax calculation features for the delivery process on Odoo eCommerce.

Click on the :guilabel:`Install` button on the module labeled :guilabel:`Avatax`: `account_avatax`.
This will install the following modules:

- :guilabel:`Avatax`: `account_avatax`
- :guilabel:`Avatax for SO`: `account_avatax_sale`
- :guilabel:`Account Avatax - Ecommerce`: `website_sale_account_avatax`

Should *AvaTax* be needed for Odoo *Subscriptions* or for delivery tax in Odoo *Ecommerce*, then
install those modules individually by clicking on :guilabel:`Install`. Additionally, in Brazil, two
separate *AvaTax* modules need to be installed. See the list above for these modules.

.. _avatax/credentials:

Odoo AvaTax settings
====================

To integrate the *AvaTax* :abbr:`API (application programming interface)` with Odoo, go to
:menuselection:`Accounting --> Configuration --> Settings` section. The :guilabel:`AvaTax` fields in
the :guilabel:`Taxes` section is where the *AvaTax* configurations are made and the credentials are
entered in.

.. image:: avatax/avatax-configuration-settings.png
   :align: center
   :alt: Configure Avatax settings

Prerequisites
-------------

First, select the :guilabel:`Environment` that the company wishes to use AvaTax in. It can either be
:guilabel:`Sandbox` or :guilabel:`Production`.

.. seealso::
   For help determining which *AvaTax* environment to use (either :guilabel:`Production` or
   :guilabel:`Sandbox`), visit: `Sandbox vs Production environments
   <https://knowledge.avalara.com/bundle/fzc1692293626742/page/sandbox-vs-production.html>`_.

Credentials
-----------

Now, the credentials can be entered in. The AvaTax :guilabel:`Account ID` will be entered in the
:guilabel:`API ID` field and the :guilabel:`License Key` will be entered in the :guilabel:`API Key`
field.

.. important::
   The :guilabel:`Account ID` can be found by logging into the AvaTax portal (`sandbox
   <https://sandbox.admin.avalara.com/>`_ or `production <https://admin.avalara.com/>`_). In the
   upper-right corner, click on the initials of the user and :guilabel:`Account`. The
   :guilabel:`Account ID` is listed first.

   To access the :guilabel:`License Key` see this documentation:
   :ref:`avatax/create_avalara_credentials`.

For the :guilabel:`Company Code` field enter the Avalara company code for the company being
configured. Avalara interprets this as `DEFAULT` if it is not set. The :guilabel:`Company Code` can
be accessed in the Avalara management portal.

First, log into the AvaTax portal (`sandbox
<https://sandbox.admin.avalara.com/>`_ or `production <https://admin.avalara.com/>`_). Then,
navigate to :menuselection:`Settings --> Manage Companies`. The :guilabel:`Company Code` value is
located in the row of the :guilabel:`Company` in the :guilabel:`Company Code` column.

.. image:: avatax/company-code.png
   :align: center
   :alt: AvaTax company code highlighted on the company details page.

Transaction options
-------------------

There are two transactional settings that can be configured: :guilabel:`Use UPC Commit` and
:guilabel:`Commit Transactions`.

If the checkbox next to :guilabel:`Use UPC codes` is ticked then, the transactions will use
Universal Product Codes (UPC), instead of custom defined codes in Avalara. Consult a certified
public accountant (CPA) for specific guidance.

Should the :guilabel:`Commit Transactions` checkbox be ticked, then, the transactions in the Odoo
database will be committed for reporting in AvaTax.

Address validation
------------------

The *address validation* feature ensures that the most up-to-date address by postal standards is set
on a contact in Odoo. This is important to provide accurate tax calculations for customers.

.. important::
   The :guilabel:`Address Validation` feature only works with partners/customers in North America.

Additionally, tick the checkbox next to the :guilabel:`Address validation` field.

.. important::
   For accurate tax calculations, it is best practice to enter a complete address for the contacts
   saved in the database. However, AvaTax can still function by implementing a best effort attempt
   using only the :guilabel:`Country`, :guilabel:`State`, and :guilabel:`Zip code`. These are the
   three minimum required fields.

:guilabel:`Save` the settings to implement the configuration.

.. tip::
   Manually :guilabel:`Validate` the address by navigating to :menuselection:`Contacts app` and
   selecting a contact. Now that the AvaTax module have been configured on the database, a
   :guilabel:`Validate` button appears directly below the :guilabel:`Address`.

   Click :guilabel:`Validate` and a pop-up window appears with a :guilabel:`Validated Address` and
   :guilabel:`Original Address` listed. If the :guilabel:`Validated Address` is the correct mailing
   address for tax purposes click :guilabel:`Save Validated`.

   .. image:: avatax/validate-address.png
      :align: center
      :alt: Validate address pop-up window in Odoo with "Save Validated" button and "Validated
            Address" highlighted.

.. warning::
   All previously entered addresses for contacts in the Odoo database will need to be validated
   using the manually validate process outlined above. Addresses are not automatically validated if
   they were entered previously. This only occurs upon tax calculation.

Sync parameters
---------------

Upon finishing the configuration and settings of the AvaTax section click the :guilabel:`Sync
Parameters` button. This action will synchronize the exemption codes from AvaTax.

.. _avatax/fiscal_positions:

Fiscal position
===============

Next, navigate to :menuselection:`Accounting app --> Configuration --> Accounting: Fiscal
Positions`. A :guilabel:`Fiscal Position` is listed called :guilabel:`Automatic Tax Mapping
(AvaTax)`. Click it to open AvaTax's fiscal position configuration page.

Here, ensure that the :guilabel:`Use AvaTax API` checkbox is ticked.

Optionally, tick the checkbox next to the field labeled: :guilabel:`Detect Automatically`. Should
this option be ticked, then, Odoo will automatically apply this :guilabel:`Fiscal Position` for
transactions in Odoo.

Enabling :guilabel:`Detect Automatically` also makes specific parameters, such as :guilabel:`VAT
required`, :guilabel:`Foreign Tax ID`, :guilabel:`Country Group`, :guilabel:`Country`,
:guilabel:`Federal States`, or :guilabel:`Zip Range` appear. Filling this parameters will filter the
:guilabel:`Fiscal Position` usage. Leaving them blank will ensure all calculations are made using
this :guilabel:`Fiscal Position`.

.. warning::
   Should the :guilabel:`Detect Automatically` checkbox not be ticked, then each customer will need
   to have the :guilabel:`Fiscal Position` set on their :guilabel:`Sales and Purchase` tab of the
   contact record. To do so, navigate to :menuselection:`Sales app --> Order --> Customers` or
   :menuselection:`Contacts app --> Contacts`. Then select and customer or contact to set the fiscal
   position on.

   Navigate to the :guilabel:`Sales and Purchase` tab and down to the section labeled
   :guilabel:`Fiscal Position`. Set the :guilabel:`Fiscal Position` field to the fiscal position
   for the customer.

.. seealso::
   :doc:`fiscal_positions`

AvaTax accounts
---------------

Upon selecting the checkbox option for :guilabel:`Use AvaTax API` a new :guilabel:`AvaTax` tab
appears. Click into this tab to reveal two different settings.

The first setting is the :guilabel:`AvaTax Invoice Account`, while the second is, :guilabel:`AvaTax
Refund Account`. Ensure both accounts are set for smooth end-of-year record keeping. Consult a
certified public accountant (CPA) for specific guidance on setting both accounts.

Click :guilabel:`Save` to implement the changes.

Tax mapping
===========

The AvaTax integration is available on sale orders and Invoices with the included AvaTax fiscal
position.

Product category mapping
------------------------

Before using the integration, specify an :guilabel:`Avatax Category` on the product categories.
Navigate to :menuselection:`Inventory --> Configuration --> Product Categories`. Select the product
category to add the :guilabel:`AvaTax Category` to. In the :guilabel:`AvaTax Category` field, select
a category from the drop-down menu, or :guilabel:`Search More...` to open the complete list of
options.

.. image:: avatax/avatax-category.png
   :align: center
   :alt: Specify AvaTax Category on products.

Product mapping
---------------

AvaTax Categories may be set on individual products as well. To set the :guilabel:`Avatax Category`
navigate to :menuselection:`Inventory app --> Products --> Products`. Select the product to add the
:guilabel:`Avatax Category` to. Under the :guilabel:`General Information` tab, on the far-right, is
a selector field labeled: :guilabel:`Avatax Category`. Finally, click the drop-down menu and select
a category, or :guilabel:`Search More...` to find one that is not listed.

.. note::
   If both the product and its category have an AvaTax Category set, the product's AvaTax Category
   takes precedence.

.. image:: avatax/override-avatax-product-category.png
   :align: center
   :alt: Override product categories as needed

.. important::
   Mapping an :guilabel:`AvaTax Category` on either the *Product* or *Product Category* should be
   completed for every *Product* or *Product Category*, depending the route that is chosen.
