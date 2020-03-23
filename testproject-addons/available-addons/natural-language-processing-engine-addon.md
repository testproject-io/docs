# Natural Language Processing Engine Addon

This addon gives you access to a Natural Language Processing \(NLP\) Engine that converts "Plain English" sentence commands into executable code. It features the [Magic Object Model](https://candymapper.com/the-magic-object-model) for on-the-fly object recognition of visible Links, Buttons, Fields, Lists, Tabs, CheckBoxes, RadioButtons and Text.

### Magic Object Model Word

#### Verbs 

The framework supports the following list of verbs:

* `Open` \[any URL\], 
* `Hover` - Specify a named Button, Link, Tab or Field 
* `Click` - Specify a named Button, Link, Tab, Field, Image, RadioButton or Checkbox 
* `Select` - Specify a named Item from a named List 
* `Enter` -  Put the specified Text into the specified Field 
* `Clear` - Clear a named Checkbox 
* `Type` - This command will type text at current element.  For example: `Click Name Field Type Paul`It also allow PgUp, PgDn, Up, Down keys to be sent to the browser to perform custom scrolling. For example: `Click 'Show All Images' Type PgUp`The phrase `Type Esc` can be used to clear most popups.
* `Wait` - Pauses execution for a stated amount of seconds 
* `Wait For` - Waits up to 9 seconds for a text element to appear 
* `Verify` - Specify any named element

There are also some alternative verb sets that can be used.

`Nav To` and `Navigate To` are alternates to the Open Verb. `Set` is an alternate to Enter  and `Hover Over` is an alternate to Hover. Also, `Is Displayed` and `Is Visible` are alternates to Exists and `Is Not Displayed` and `Is Not Visible` are alternates to Does Not Exist

#### Verify

The Verify verb supports the following element validations:

* Verify Named \[Element Type\] is enabled 
* Verify Named \[Element Type\] is displayed 
* Verify Named Field is 'Expected Text' \(Exact match - case sensitive\) 
* Verify Named Field Contains 'Expected Text' \(Close match - case sensitive\)

### Sentence Parsing

The basic structure consists of a basic two to five word sentence

`[Verb] [Element Name] [Class] [Verify] [Data]`

For example each of the following commands are valid:

* "Open [https://candymapper.com/the-magic-object-model](https://candymapper.com/the-magic-object-model)" 
* "Click Send Button" 
* "Enter Name Field Paul" 
* "Verify Name Field Contains Paul"
*  "Select Vehicle List Audi"

### Advanced Parsing 

The NLS engine can also parse more verbose sentences, for example you could include phrases like:

* "Click on the Send Button" 
* "Verify the Name Field Contains Paul"

### Alternative Sentence Structure

Select and Enter verbs support a natural alternative sentence structure: 

`[Verb] [Data] [Element Name] [Class]`

For example the following commands are valid:

* "Select Audi from Vehicle List" 
* "Enter Paul into the Name Field"

### Deductive Class Reasoning

If no object class is included the framework uses deductive reasoning to guess element types in shorter form sentences.

For example if you type "Click Send"  it will guess that type as `Button` 

Some other examples could look this:

* Select Audi from Vehicle" \(Assume: `List`\) 
* "Verify Name Contains Paul" \(Assume `Field`\) 
* "Verify Paul" \(Assume `Text, Exists`\)

### Tips and Tricks

#### Single Quotes

 Single quotes are supported where a named element includes an class. For example: `Verify 'Naughty and Nice List' Text exists` 

#### Negative Testing

`Verify` also supports negative testing. For example: 

* `Verify 'Expected Text' does not exist` 
* `Verify Named Button is not displayed` 
* `Verify Named Field does not contain 'Expected Text'` 

#### Highlighting

The engine uses brief highlighting for visual validation during execution Pass results are highlighted briefly in Green. Failed results highlight in Red and pauses for 3 seconds.

If more than one image element matched your text, any other on screen matches will be highlighted for a few seconds and a First Close Match warning will be reported. In this case consider a using longer string to uniquely identify elements.

#### Comments

Comments can be added to the output with the `comment` command. For example:`Comment 'Populate the Shopping Cart'`

#### Case Sensitivity

Text and Links are the only elements that have case insensitive matches. All other elements must match in case sensitivity.

**Tip**: Use F12 to review the exact element wording in the HTML page. Sometimes the case of the displayed text does not match that of the HTML.

#### Class Switching

 If no Button element can be found a class switch to a Link will be executed. If, in that case, a match is found a Warning is output into the results. The same thing is done in reverse for Links as for Buttons.

If no text element can be found a class switch to all elements will be executed. If a match is then found a Warning is output into the results.

