---
text: "TrailHead"
title: "Salesforce Training"
author: "Peter Farrar"
date: 04/14/2025
description: "Notes on Salesforce training on TrailHead"
---

# SalesForce/TrailHead

## Create a custom object

1. Click on the setup menu icon (a small cog in the top right corner of the screen)
2. Select `Setup`
3. Select the `Object Manager` tab (top right)
4. Click `Create` (top right corner) then select `Custom Object`
5. Enter a value for `Label` and press the TAB key (this will auto populate the `Field Name`)
6. Enter a value for `Plural Label`
7. Scroll to the bottom of the page and select the check box next to `Launch New Custom Tab Wizard after saving this custom object`
8. Click `Save` (bottom center menu)
9. Click in the `Tab Style` box and select an icon from the modal pop-up
10. Click `Next` (bottom right menu)
11. Click `Next`
12. Click `Save`

That's it.  

---

## Add a field to an object

1. Click on the setup menu icon (a small cog in the top right corner of the screen)
2. Select `Setup`
3. Select the `Object Manager` tab (top right)
4. Scroll through the list of objects until you find the object you want to modify
5. Select `Fileds & Relationships`
6. Click `New` (top right menu)
7. Under `Data Type` select the radio button next to the data type you want to use
8. Click `Next`
9. Enter a value for `Field Label` and press the TAB key (this will auto populate the `Field Name`)
10. Click `Next`
11. Click `Next` again to except field-level security settings
12. Click `Save` (top right menu)

That's it.  

---

## Create a record

Assume the object `Property` has been defined  

1. Select the App in `App Launcher`
2. Click on the `Properties` tab
3. Click `New` (top right menu)
4. Fill in the required fields
5. Click `Save` 

This creates a new instance of type `Property`   

---

## Create a Lookup relationship

1. Create a new field on an object of type `Lookup Relationship`
2. Click `Next`
3. For the `Related To` dropdown, select the object you want this object to have a lookup relationship with
4. Click `Next`
5. `Field Label` should be populated with the name of the object you are creating a relationship with. You can customize this field.
6. Press TAB to populate the `Field Name`
7. Click `Next`
8. Click `Next`
9. Click `Next`
10. Click `Save`

That's it.

---

## Create a Master-Detail relationship

1. Create a new field on an object of type `Master-Detail Relationship`
2. Click `Next`
3. From the `Related To` dropdown, select the object that you want to be the **Master** object of the object you are editing.
4. Click `Next`
5. `Field Label` should be populated with the name of the object you are creating a relationship with. You can customize this field.
6. Press TAB to populate the `Field Name`
7. Click `Next`
7. Click `Next`
7. Click `Next`
7. Click `Save`

That's it.

---

## Create a detail record for a master-detail relationship

1. In the app, choose the master field.
2. Click on the record that you want to add detail records to
3. Select the `Related` tab
4. Click `New`
5. Enter a name in the name field
6. Click `Save`

That's it.

---

## Import data into SalesForce

* Data Import Wizard
* Data Loader

### Data Import Wizard

* Loads up to 49,999 records
* Supports many object types
* Runs interactively

### Data Loader

* Loads up to 150,000,000 records
* Supports all object types
* Can be automated

#### Salesforce data import guidelines  

* Use existing software to export a file in .csv
* Clean up data in the csv file. Remove duplicates and unnecessary information. Check data for accuracy and consistancy. Correct spelling and other errors. Enforce naming conventions.
* Compare fields with the Salesforce fields you want to import into. Verify the fields will be mapped into the correct fields. You may need to fine tune the mapping first. You can find information to help you with that [here](https://help.salesforce.com/s/articleView?language=en_US&id=sf.field_mapping_for_other_data_sources_and_organization_import.htm&type=5&_ga=2.222256024.1234867830.1744045172-73680456.1743707792)
* Make any configurations required to handle the imported data.

It is recommended to test imports with a small file first, to insure everything is mapping correctly.  

Remember to turn off any workflows you don't want to fire when performing imports.  

### Using the Data Import Wizard

#### Start the wizard

1. From Setup, ender Data Import Wizard in the Quick Find box. Select **Data Import Wizard**.
2. Review the welcome page. Click **Launch Wizard**.

#### Choose the data to import

1. To import accounts, contacts, leads, solutions, person accounts, or campaign members, click **Standard Objects**. For other objects click **Custom Objects**.
2. Specify _add new records_, _update existing records_, or _add and update records_.
3. Specify matching and other criteria.
4. Specify the file to import, either by drag-and-drop or click and navigate.
5. Choose the character encoding method.
6. Click **Next**.

#### Map data fields to Salesforce data fields

The wizard tries to guess as many data field types as it can. Verify these are correct and map the other field types manually.  

1. Scan the list of mapped fields.
2. Click **Map** to the left of each unmapped field.
3. Choose the Salesforce fields from the dialog box and click **Map**.
4. For fields that were incorrectly mapped automatically, click **Change** and select the appropriate type and click **Map**.
5. Click **Next**.

#### Review and start import

1. Review information on the Review page. If you need to make changes click **Previous**.
2. Click **Start Import**.

#### Check the import status

Enter "Bulk Data Load Jobs" in the Quick Find Box and select **Bulk Data Load Jobs**.

* Multi-Select Picklists: To import multiple values into a multi-select picklist, separate the values by a semicolon in your import file.
Checkboxes—To import data into a checkbox field, use 1 for checked values and 0 for unchecked values.
* Default Values: For picklist, multi-select picklist, and checkbox fields, if you do not map the field in the import wizard, the default value for the field, if any, is automatically inserted into the new or updated record.
* Date/Time Fields: Ensure that the format of any date/time fields you are importing matches how they display in Salesforce per your locale setting.
Formula Fields—Formula fields cannot accept imported data because they are read-only.
* Field Validation Rules: Salesforce runs validation rules on records before they are imported. Records that fail validation aren’t imported. Consider deactivating the appropriate validation rules before running an import if they affect the records you are importing.

---

## Export data out of SalesForce

* Data Export Service
* Data Loader

### Using the Data Export Service

1. From Setup, enter "Data Export" in the Quick Find box, then select **Data Export** and **Export Now** or **Schedule Export**.
   * Export Now exports immediately, if enough time has elapsed since the last export.
   * Schedule Export schedules an export to run at monthly intervals
2. Select an encoding for the export file
3. Select options for any attachments
4. Optionally select Replace carriage returns with spaces
5. If scheduling exports, select frequency, start and end dates, and time of day
6. Under Exported Data, select the types of data to export (**Include all data** is recommended if you're not sure)
7. Click **Start Export** or **Save**. You will receive an email when the export is completed.

Exports are created in a zip file. The zip file is deleted 48 hours after the export completes.  

---

## Create a Lightning App

1. Use the gear icon to find the Setup App
2. In the Quick Find Box type `App` and select App Manager.
3. In the Top right corner of the App Manager, click **New Lightning App**
4. Fill in details in the Wizard and click **Next**
5. On App Options, click **Next**
6. On Utility Items, click **Next**
7. Add navigation items (For this demo add: Home, Chatter, Groups, Energy Audits, Accounts, Contacts, Products, Tasks) and click **Next**
8. In User Profile select "System Administrator" This is not how to do it in production, just for learning in a sandbox.
9. Click **Save and Finish**

That's it.  

---

## Create and Customize View Lists

### Create a List View

1. In the App Launcher (top left) Enter `Sales` and select the Sales app, then click on the Accounts tab.
2. The list view controls is a drop down in the top right corner with a gear like icon. Click on that and select 'New'.
3. Name the list and select **All users can see this list view**.
4. Click **Save**.
5. In the top right, click on the funnel icon and select **Add Filter**.
6. Select your criteria (For this example we selected Type equals Customer - Channel) then click **Done**
7. Click **Save**.
8. Add a second filter (inthis case State/Province equals "WA,OR,CA")

### Customize a List View

1. The list view controls is a drop down in the top right corner with a gear like icon. Click on that and select 'Select Fields to Display'.
2. Move fields to and from Available Fields/Visible Fields. Click **Save**.

**Note:** Hover over cells. If there is a pencil icon on the right side of the cell, you can directly edit that cell in the list. If there is a padlock, you can not.  

### Create a List View Chart

In this example there is assumed to be an existing sales app.

1. Click on the Opportunities tab.
2. Use the dropdown menu (Top right downward facing triangle, next to the Page Heading) to select **All Opportunities**.
3. Click the charts menu (Top left... I think it's supposed to look like a pie chart?). A Charts menu will appear.
4. Select the gear icon in the Charts menu and select **New Chart**.
5. Name the chart. Select the chart type (Donut), Aggregate Type and Field (Sum/Amount), abd Grouping Field (Account Name).
6. Click **Save**.

### Resources:

* [Salesforce Help: Create or Clone a List View in Lightning Experience](https://help.salesforce.com/HTViewHelpDoc?id=customviews_lex.htm&language=en_US&_ga=2.239595207.574000836.1744657100-73680456.1743707792)
* [Salesforce Help: Edit List View Filters in Lightning Experience](https://help.salesforce.com/HTViewHelpDoc?id=customviews_edit_filters_lex.htm&language=en_US&_ga=2.239595207.574000836.1744657100-73680456.1743707792)
* [Salesforce Help: Create a List View Chart in Lightning Experience](https://help.salesforce.com/HTViewHelpDoc?id=customviews_listview_chart_create_lex.htm&language=en_US&_ga=2.239595207.574000836.1744657100-73680456.1743707792)
* [Salesforce Help: Update Records Inline from a List View in Lightning Experience](https://help.salesforce.com/HTViewHelpDoc?id=customviews_edit_inline_listview_lex.htm&language=en_US&_ga=2.38873831.574000836.1744657100-73680456.1743707792)

---

## Customize Record Highlights with Compact Layouts

### Create a Compact Layout

1. From Setup click **Object Manager** and select the object to build a compact layout for (Energy Audit)
2. Click Compact Layouts (left side menu)
3. Click **New** (top right corner)
4. Give the Label a name (Energy Audit Compact Layout). **Tab** will auto populate the name field.
5. Add fields to the layout using the **Select Compact Layout Fields** menu and click **Save**
6. Click **Compact Layout Assignment** and then **Edit Assignment**
7. Select the layout from the **Primary Compact Layout** dropdown and click **Save**

That's it. The compact layout form is used at the top of record pages, and on mobile.  

### Resources:

* [Salesforce Help: Compact Layouts](https://help.salesforce.com/HTViewHelpDoc?id=compact_layout_overview.htm&language=en_US&_ga=2.39174887.574000836.1744657100-73680456.1743707792)
* [Salesforce Help: Notes on Compact Layouts](https://help.salesforce.com/HTViewHelpDoc?id=compact_layout_notes.htm&language=en_US&_ga=2.39174887.574000836.1744657100-73680456.1743707792)
* [Salesforce Help: Assign Compact Layouts to Record Types](https://help.salesforce.com/HTViewHelpDoc?id=compact_layout_assign.htm&language=en_US&_ga=2.34605669.574000836.1744657100-73680456.1743707792)

---

## Customize Record Page Components and Fields

### Edit a Record Layout

1. From the App Launcher, the your application to modify
2. Select the tab containing the record whos layout will be modified
3. Select a record
4. Change the API name if you are creating a new kind of record
5. Click the Details tab
6. On the right side, click **Upgrade Now**
7. Select the layout you want and click **Finish**
8. Move fields about, or delete as required
9. Click Save
10. Click **Not Yet** if the page shouldn't be finished yet

### Customize Related Lists

1. From **Setup** click Object Manager, then find the object to deit
2. Click **Page Layouts** and select the layout to modify
3. Here you can click **Related Lists** and drag a Files element into the Related List section. There are other kinds of lists as well.
4. Click *Quick Save** and **Yes**

### Activate a Page

1. From Setup click the Home tab
2. Search for `App Builder` in the Quick Find box and select **Lightning App Builder**
3. Click Edit next to the Record Page to activate
4. Click **Activation**
5. Select the options desired for the page
6. Verify the selection
7. Click **Save**

You may need to refresh the page to see the changes  

