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

# Create a detail record for a master-detail relationship

1. In the app, choose the master field.
2. Click on the record that you want to add detail records to
3. Select the `Related` tab
4. Click `New`
5. Enter a name in the name field
6. Click `Save`

That's it.

---
