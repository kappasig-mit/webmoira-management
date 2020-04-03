# MIT Web Moira Mailing List Management
A Python and bash-based helper tool for automating the addition and deletion of members from MIT Web Moira lists.

## Installation
Simply clone this repo, and make sure you have `ssh`, `scp`, and Python set up on your command line!  These scripts were run and developed on Ubuntu 18.04, but should work on any operating system.

## Use
This tool features an automated WebMoira client for updating email lists, as well as a tool for sending automated emails with user-specific information (`email_user_information.py`).  Each of these features are discussed below.

### Automating User Information Emails
Have a spreadsheet with user-specific information you want to send out?  You've come to the right place.  The Python file `email_user_information.py` allows you to read a spreadsheet file with email addresses and user information columns, and send out emails to each user with their specific user information.
   
**NOTES**: 

1. You'll need to edit the `body` variable in the function `mail_to_list` to create the body of the email.

2. Make sure you enable less secure google apps for the specific gmail address you're using.  See the link [here](https://myaccount.google.com/lesssecureapps).
 
3. You'll likely need to edit how user-specific information is read in from the spreadsheet (i.e. edit the `df` object in the main function).
 
 Once ready, you can test your script with (the script will print the email information to the Python console):
 
```python email_user_information.py <gmail> <gmail_password> <email_subject> <path/to/file.xlsx> --test```
 
 And once you're satisfied with the quality of your emails, you can send them by simply removing the `--test` flag:
  
```python email_user_information.py <gmail> <gmail_password> <email_subject> <path/to/file.xlsx>```

### Automating the WebMoira Tool
One of the primary uses of this repository is to automatically add or delete many members from a MIT Web Moira email list at once (for adding/deleting only a couple of members at a time, check out the [WebMoira Tool](https://groups.mit.edu/webmoira/).  

This codebase uses command-line arguments to determine what email management actions should be taken.  Commands can be selected by calling the Python file in a command line environment:

```python manage_emails.py <kerberos> <mailing_list> -d -a -t -f```

Where:

1. `<kerberos>` is your kerberos (or someone else with admin access to the WebMoira list you're modifying).  (Required.)
2. `<mailing_list>` is the WebMoira list you're modifying. (Required.)
3. `-d` is an optional flag indicating you want to delete members from `<mailing_list>`.
4. `-a` is an optional flag indicating you want to add members to `<mailing_list>` (note: this requires you to input a file path to a file of kerberoses as well).
5. `-f` is an optional argument for inputting a path to a text file indicating the line-separated kerberoses you want to add to `<mailing_list>`.
6. `-t` is an optional flag indicating that you want to transfer the bash files over to your athena account (this only needs to be done once, but it must be done the first time you add or delete members).

Below are the flag configurations you should use for adding and deleting members (note that you don't need the `-t` flag if you've already run these commands with the `-t` flag at least once).

**Adding a list of members**:
```python manage_emails.py <kerberos> <mailing_list> -a -t -f <path/to/names.txt>```

**Deleting a list of members**:
```python manage_emails.py <kerberos> <mailing_list> -d -t```

**Creating a text file of members to add**: See the file `sample_kerb_file.txt` for an example on how this should be formatted.


