# Python-Password-Manager

## Script Requirements
When making this python password manager, I wanted the script to have the following features:
- Have an options menu:
    - Add credentials (username, password, URL)
    - View stored credentials
    - Exit the script
- Menu Navigation: Return to the menu after each action has completed
- Formatted Output: Display the contents of the text file in a clear and visually organized format, using proper spacing and headings.
- Credential Storage: Create a text file for credential storage if a text file does not already exist and append new records to the text file without overwriting previous entries
- Error Handling: Handle any input from the user and carry out actions, without errors.

I also decided to follow these rules for clarity:
- Include embedded explanatory comments (#) to clarify the meaning of the code where necessary
- Follow the PEP 8 Style Guide
## Pseudo-code
```
define function home
 repeat if called (as to return to the menu after each action has completed)
  display "options menu"
  display "1.add user information"
  display "2.view user information"
  display "3.exit password manager"
  display "please choose between 1-3"
(this displays the options menu and the choices that the user will have)
  get choice from user input
  if choice = 1
  call function adduserinformation
  if choice = 2
  call function viewuserinformation
  if choice = 3 
  display "exiting password management script"
  exit the script by breaking the loop 
  otherwise
   display "invalid input choose between 1-3"

define function adduserinformation
  define variable 'url' from user input while showing "please enter website"
  define variable 'username' from user input while showing "please enter username"
  define variable 'password' from user input while showing "please enter password"

  open the file "stored_credentials.txt" in append mode
  write in the file "website: variable:url, Username: variable:username, password: variable:password" (variable:url means listing what has been inputted when asked previously)
  close file
  display "information has been stored"

define function viewuserinformation
 try to (as to allow for the error handling "if file is not found")
  open file "stored_credentials.txt" in read mode
  read data from file
  display "stored information"
  display data
  close file
 if file is not found
 display "file has not been found. text file will be created upon storing information"
 go back to main menu

call the function home
```
## Actual Code

```
#FILE NAME IS: "stored_credentials.txt"
def home():
    #Displays the start menu and the choices that you have, exits script upon choosing 3 and tells you if you have inputted an invalid character

    while True:
        print("\tOptions Menu")
        print("1. Add User Information")
        print("2. View User Information")
        print("3. Exit Password Manager")
        print("Please input an option (1-3)")
        choice = input()
        if choice == '1':
            add_user_information()
        elif choice == '2':
            view_user_information()
        elif choice == '3':
            print("Exiting Password Management Script")
            break
        else:
            print("Invalid Input, please enter an option through 1-3:")

def add_user_information():
    #If the user chooses to add user information, by defining the option it allows for the script to return the required text.

    url = input("Please enter the website:")
    username = input("Please enter your username:")
    password = input("Please enter your password:")

    with open ("stored_credentials.txt", "a") as file:
        file.write(f"Website: {url}, Username: {username}, Password: {password}\n\n")
        print("Information has been stored. File has been created or modified.")
      #Opens a file and writes the inputs given, while formatting it neatly with headings.

def view_user_information():
#If the user wants to look at previously inputted passwords for a website, they would choose this and this will display what is currently written in the file (file is in read mode)

    try:
        with open ("stored_credentials.txt", "r") as file:
            data = file.read()
            print("Stored Information")
            print(data)
       
    except FileNotFoundError:
        print("No information has been stored yet. Text file will be created upon storing information")
        return
    
    
    #This will tell the user if any information has not been stored yet.
home()
```
