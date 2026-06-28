# Update a file through a Python algorithm

## Project description
A security analyst is tasked with managing an 'allow list' of IP addresses that are used by employees to access sensitive information. 
There are two lists that are required to be compared. The 'allow list' must be checked for any IP's that are included in the 'remove list'.

## Code
```
# assign allow text file to import_allow variable
import_allow = "allow_list.txt"

# assign remove list IP's to remove_list variable
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

# open the text file in read mode and assign it a temporary variable called allow
with open(import_allow, "r") as allow:

     # save the text from the file to a variable called allow_text
       allow_text = allow.read()

# convert the text string to a list
allow_text = allow_text.split()

# iterate through allow list
for ip in allow_text:

    # remove IP addresses that are on the remove list
    if ip in remove_list:
        allow_text.remove(ip)

# turn the amended list back into a string
allow_text = " ".join(allow_text)

# open the original file, this time in write mode and assign to a variable
with open(import_allow, "w") as allow:

    # write the updated list to the file
    allow.write(allow_text)
```

## Summary
The script above automates the removal of IP addresses included on the 'remove list' from the 'allow list'. This is an effective way to reduce human error and remove a repetitive, time consuming task from an analysts workload. 

The script performs the following tasks:
Imports the allow list file
Parses it into a list
Iterates through each item in the allow list and checks it against the items in the remove list
Removes any items that match the remove list
Turns the updated list back into writable string
Overwrites the old list with the new list in the text file

## Skills Demonstrated
```Python```, ```Automation```, ```Access Control Management```
