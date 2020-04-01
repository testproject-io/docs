# Random Login Credentials Addon

This addon generates random credentials for login forms. You can generate random email address, random password and username. You can control the length, characters and the domain of the email address, control the password length and characters type and control the user name as well.

### Available Actions

`Random Email Address` - Generate random email address

This action takes in the following inputs:

* `LocalPart` - A custom local-part string \(optional\)
* `Domain` - A custom domain \(optional\)
* `LocalPartLength` - Specify the length of the local-part \(a number between 5-15\)
* `IsLower` - Include lower-case characters? \(true/false\)
* `IsUpper` - Include upper-case characters? \(true/false\)
* `IsSpecial` - Include special characters? \(true/false\)

`Random Password` - Generate random password

This action takes in the following inputs:

* `PasswordLength` - Choose the password length \(a number between 8-15\)
* `SpecialCharacters` - Include special characters? \(true/false\)
* `Digits` - Include digits? \(true/false\)
* `UpperCase` - Include upper-case letters? \(true/false\)
* `LowerCase` - Include lower-case letters? \(true/false\)

`Random Username` - Generate random username

This actions take in the `Length` input where you can enter the username length \(as a number between 3-12\). The default for this, if you do not specify anything, is 6 characters

