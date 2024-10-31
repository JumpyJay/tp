---
layout: page
title: User Guide
---

PhysioPal is a **desktop app for managing contacts for physiotherapists, optimized for use via a Command Line Interface**
(CLI) while still having the benefits of a Graphical User Interface (GUI). If you can type fast, PhysioPal can get
your contact management tasks done faster than traditional GUI apps.

* Table of Contents
{:toc}

--------------------------------------------------------------------------------------------------------------------

## Quick start

1. Ensure you have Java `17` or above installed in your Computer.

1. Download the latest `.jar` file from [here](https://github.com/se-edu/addressbook-level3/releases).

1. Copy the file to the folder you want to use as the _home folder_ for your AddressBook.

1. Open a command terminal, `cd` into the folder you put the jar file in, and use the `java -jar addressbook.jar` command to run the application.<br>
   A GUI similar to the below should appear in a few seconds. Note how the app contains some sample data.<br>
   ![Ui](images/Ui.png)

1. Type the command in the command box and press Enter to execute it. e.g. typing **`help`** and pressing Enter will open the help window.<br>
   Some example commands you can try:

   * `list` : Lists all contacts.

   * `add n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01` : Adds a contact named `John Doe` to the Address Book.

   * `delete John Doe` : Deletes the contact named `John Doe` in the current list.
   
   * `schedule John Doe d/2024-10-14 1200 note/First appointment`: Schedules an appointment for John Doe on October 14, 2024, at 12pm with the given note.

   * `appointment-delete John Doe d/2024-10-14 1200` : Deletes a specified appointment for John Doe.

   * `appointment-list` : Lists all upcoming scheduled appointments.

   * `reminder John Doe r/1 hour` : Sets a reminder for John Doe 1 hour before his scheduled appointment.

   * `reminder-delete John Doe` : Deletes the reminder set for John Doe.

   * `payment John Doe d/2024-10-14 1200 pay/paid`: Marks the appointment for John Doe on October 14, 2024, at 12pm as paid.

   * `clear` : Deletes all contacts.

   * `exit` : Exits the app.

1. Refer to the [Features](#features) below for details of each command.

--------------------------------------------------------------------------------------------------------------------

## Features

<div markdown="block" class="alert alert-info">

**:information_source: Notes about the command format:**<br>

* Words in `UPPER_CASE` are the parameters to be supplied by the user.<br>
  e.g. in `add n/NAME`, `NAME` is a parameter which can be used as `add n/John Doe`.

* Items in square brackets are optional.<br>
  e.g `n/NAME [t/TAG]` can be used as `n/John Doe t/anklesprain` or as `n/John Doe`.

* Items with `…`​ after them can be used multiple times including zero times.<br>
  e.g. `[t/TAG]…​` can be used as ` ` (i.e. 0 times), `t/anklesprain`, `t/anklesprain t/acltear` etc.

* Parameters can be in any order.<br>
  e.g. if the command specifies `n/NAME p/PHONE_NUMBER`, `p/PHONE_NUMBER n/NAME` is also acceptable.

* Extraneous parameters for commands that do not take in parameters (such as `help`, `list`, `exit` and `clear`) will be ignored.<br>
  e.g. if the command specifies `help 123`, it will be interpreted as `help`.

* If you are using a PDF version of this document, be careful when copying and pasting commands that span multiple lines as space characters surrounding line-breaks may be omitted when copied over to the application.
</div>

### Viewing help : `help`

Shows a message explaning how to access the help page.

![help message](images/helpMessage.png)

Format: `help`


### Adding a person: `add`

Adds a person to the address book.

Format: `add n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [t/TAG]…​`

<div markdown="span" class="alert alert-primary">:bulb: **Tip:**
A person can have any number of tags (including 0)
</div>

Examples:
* `add n/John Doe p/98765432 e/johnd@example.com a/John street, block 123, #01-01`
* `add n/Betsy Crowe t/acltear e/betsycrowe@example.com a/Newgate Prison p/1234567 t/anklesprain`

### Scheduling an appointment: `schedule`

Schedules an appointment for a client in the address book.

Format: `schedule NAME d/DATE_AND_TIME…​ note/NOTES…​`

* You can schedule multiple appointments using the `d/` prefix for each date and time.
* If multiple `note/` prefixes are used, each note will correspond to the `d/` in the same order. Same number of notes and dates must be provided.
* The given date must fall on a weekday.
* The given time must be on the hour between 0900 and 1700.
* Format for the date and time must be in yyyy-MM-dd HHmm.
* When scheduling appointments, the existing schedules of the person will be removed i.e adding of schedules is not cumulative.

Examples:
* `schedule John Doe d/2024-10-14 1200 note/first appointment`
* `schedule Betsy Crowe d/2024-10-14 1300 note/first appointment`
* `schedule John Doe d/2024-10-14 1200 d/2024-10-15 1300 note/important meeting note/not so important meeting`

### Setting a reminder: `reminder`

Sets a reminder for a client before their appointment in the address book.

Format: `reminder NAME r/REMINDER_TIME`

* You can only set a reminder for a person who already has a scheduled appointment.
* The reminder time must be a valid expression (e.g. "1 day", "2 hours").

Examples:
* `reminder John Doe r/10 days`
* `reminder Betsy Crowe r/3 hours`

### Deleting a reminder: `reminder-delete`

Deletes a reminder for a client in the address book.

Format: `reminder-delete NAME`

* You can only delete a reminder for a person who has at least one scheduled appointment.
* The given name must be the name of an existing client.
* You can only delete a reminder if the reminder has been set.

Examples:
* `reminder-delete John Doe`

### Deleting an appointment: `appointment-delete`

Deletes a specified appointment for a client in the address book.

Format: `appointment-delete NAME d/DATE_AND_TIME`

* The given name must be the name of an existing client.
* The given date and time must be in the format yyyy-MM-dd HHmm.
* The appointment given must be an existing appointment for the client.

Examples:
* `appointment-delete John Doe d/2024-11-24 1200`

### Viewing upcoming appointments: `appointment-list`

Lists all upcoming appointments in the order of the earliest next upcoming appointment.

Format: `appointment-list [d/DATE_AND_TIME]`

* This will only show appointments that are in the future (compared to local time now).
* The optional date and time fields act as filters.
* A time filter cannot be applied without date filter.
* Format for the date and time must be in yyyy-MM-dd HHmm.

Examples:
* `appointment-list`
* `appointment-list d/2024-10-17`
* `appointment-list d/2024-10-18 1000`

### Making Payment for an appointment: `payment`

Marks an appointment for a client as paid or unpaid.

Format: `payment NAME d/DATE_AND_TIME pay/PAYMENT_STATUS`

* Format for the date and time must be in yyyy-MM-dd HHmm.
* Payment status can be in the format [true/paid or false/unpaid].

Examples:
* `payment John Doe d/2024-10-14 1200 pay/true`
* `payment Betsy Crowe d/2024-10-14 1300 pay/unpaid`

### Listing all persons : `list`

Shows a list of all persons in the address book.

Format: `list`

### Viewing a person: `view [NAME]`

Displays the details of a person in the address book.

**Format:** `view [NAME]`

<div markdown="span" class="alert alert-primary">
Tip:
The name must match the full name exactly.
</div>

**On success:** A pop-up window will show the details including:
- Name
- Phone Number
- Email
- Address
- Condition
- Schedule

**Examples:**
* `view John Doe`
* `view Betsy Crowe`

### Editing a person : `edit`

Edits an existing person in the address book.

Format: `edit NAME [n/NAME] [p/PHONE] [e/EMAIL] [a/ADDRESS] [t/TAG]…​`

* Edits the person with the specified `NAME`. The name refers to the name shown in the displayed person list.
* At least one of the optional fields must be provided.
* Existing values will be updated to the input values.
* When editing tags, the existing tags of the person will be removed i.e adding of tags is not cumulative.
* You can remove all the person’s tags by typing `t/` without
    specifying any tags after it.

Examples:
*  `edit John Doe p/91234567 e/johndoe@example.com` Edits the phone number and email address of the person named `John Doe` to be `91234567` and `johndoe@example.com` respectively.
*  `edit Betsy Crowe n/Betsy Crower t/` Edits the person with the name `Betsy Crowe` to be `Betsy Crower` and clears all existing tags.

### Locating persons by name: `find`

Finds persons whose names contain any of the given keywords.

Format: `find [KEYWORD] [MORE_KEYWORDS] || [p/PHONE]`

* The search is case-insensitive. e.g `hans` will match `Hans`
* The order of the keywords does not matter. e.g. `Hans Bo` will match `Bo Hans`
* Only the name is searched.
* Only full words will be matched e.g. `Han` will not match `Hans`
* Persons matching at least one keyword (or parts of it) will be returned (i.e. `OR` search).
  e.g. `Hans Bo` will return `Hans Gruber`, `Bo Yang`
* Persons matching the phone number (or parts of it) will be returned

Examples:
* `find John` returns `john` and `John Doe`
* `find alex david` returns `Alex Yeoh`, `David Li`<br>
  ![result for 'find alex david'](images/findAlexDavidResult.png)
* `find p/88` returns `John Doo` (with phone number `88765432`) <br>
  ![result for 'find alex david'](images/find88.png)

### Deleting a person : `delete`

Deletes the specified person from the address book.

Format: `delete NAME`

* Deletes the person with the specified `NAME`.
* The name must be the name of an existing person.

Examples:
* `delete John Doe` deletes the person named `John Doe` in the address book.

### Clearing all entries : `clear`

Clears all entries from the address book.

Format: `clear`

### Exiting the program : `exit`

Exits the program.

Format: `exit`

### Showing Top 3 Upcoming Appointments

Automatically displays the top 3 upcoming appointments for all contacts when you open up PhysioPal.

* This feature operates automatically upon application launch, so there is no need for any user commands.
* If there are fewer than three upcoming appointments, the list will show all available appointments.

Example display:
![display for upcoming appointments](images/upcomingAppointmentDisplay.png)

### Saving the data

AddressBook data are saved in the hard disk automatically after any command that changes the data. There is no need to save manually.

### Editing the data file

AddressBook data are saved automatically as a JSON file `[JAR file location]/data/addressbook.json`. Advanced users are welcome to update data directly by editing that data file.

<div markdown="span" class="alert alert-warning">:exclamation: **Caution:**
If your changes to the data file makes its format invalid, AddressBook will discard all data and start with an empty data file at the next run. Hence, it is recommended to take a backup of the file before editing it.<br>
Furthermore, certain edits can cause the AddressBook to behave in unexpected ways (e.g., if a value entered is outside of the acceptable range). Therefore, edit the data file only if you are confident that you can update it correctly.
</div>

--------------------------------------------------------------------------------------------------------------------

## FAQ

**Q**: How do I transfer my data to another Computer?<br>
**A**: Install the app in the other computer and overwrite the empty data file it creates with the file that contains the data of your previous AddressBook home folder.

--------------------------------------------------------------------------------------------------------------------

## Known issues

1. **When using multiple screens**, if you move the application to a secondary screen, and later switch to using only the primary screen, the GUI will open off-screen. The remedy is to delete the `preferences.json` file created by the application before running the application again.
2. **If you minimize the Help Window** and then run the `help` command (or use the `Help` menu, or the keyboard shortcut `F1`) again, the original Help Window will remain minimized, and no new Help Window will appear. The remedy is to manually restore the minimized Help Window.

--------------------------------------------------------------------------------------------------------------------

## Command summary

Action | Format, Examples
--------|------------------
**Add** | `add n/NAME p/PHONE_NUMBER e/EMAIL a/ADDRESS [t/TAG]…​` <br> e.g., `add n/James Ho p/22224444 e/jamesho@example.com a/123, Clementi Rd, 1234665 t/anklesprain t/acltear`
**Clear** | `clear`
**Delete** | `delete NAME`<br> e.g., `delete John Doe`
**Schedule** | `schedule NAME d/DATE_AND_TIME…​ [note/NOTES]…​`
**Appointment Delete** | `appointment-delete NAME d/DATE_AND_TIME`<br> e.g., `appointment-delete John Doe d/2024-10-20 1100`
**Appointment List** | `appointment-list [DATE_AND_TIME]` <br> e.g., `appointment-list 2024-10-20 1100`
**Reminder** | `reminder NAME r/REMINDER_TIME`
**Reminder Delete** | `reminder-delete NAME`
**Edit** | `edit NAME [n/NAME] [p/PHONE_NUMBER] [e/EMAIL] [a/ADDRESS] [t/TAG]…​`<br> e.g.,`edit James n/James Lee e/jameslee@example.com`
**Find** | `find [KEYWORD] [MORE_KEYWORDS] / [p/PHONE]`<br> e.g., `find James Jake` `find p/8357 2348`
**Payment** | `payment NAME d/DATE_and_TIME pay/PAYMENT_STATUS` <br> e.g., `payment John Doe 2024-10-20 1100 pay/paid`
**Appointment List** | `appointment-list [d/DATE_AND_TIME]` <br> e.g., `appointment-list d/2024-10-20 1100`
**List** | `list`
**Help** | `help`
**View** | `view [NAME]`
