# Macros-Polyworks
## _Repositorio de macros simples para polyworks_

### Codigo ayuda para empezar con macros en Polyworks
```mscl
version "5.0"
############################## POLYWORKS ######################################
#
# ---- InnovMetric Software Inc.
# ---- Module  :    PolyWorks|Inspector
# ---- Version :    2020 (build 2255)
# ---- Date    :    Wednesday, March 25, 2020 - 13:57:52
#
############################## DISCLAIMER #####################################
#
# This macro script is provided "AS IS", and may contain bugs, errors, and 
# other problems that could cause system or other failures and data loss. 
# InnovMetric Software Inc. disclaims any warranty or liability obligations 
# of any kind to the user of this macro.
#
############################## DESCRIPTION ####################################
# 
# This macro is a good starting point to start developing your programming 
# skills with the PolyWorks Macro Script Command Language (MSCL). It teaches you 
# the basics to create your own macros, with a good mix between explanations 
# and examples.
#
############################## VERSIONS #######################################
#
# VERSION 1.0
# VERSION 1.1 [PW 2021 IR0] Added AND/OR/NOT
#
############################## CODE ###########################################

# Command History (Tools -> Commands -> Command History)
# ------------------------------------------------------
# Each operation performed in PolyWorks will write a corresponding command
# in the Command History. Those commands are the building blocks of macros.


# Macro Script Editor (Tools -> Macro Scripts -> Macro Script Editor)
# --------------------------------------------------------------------
# This text editor allows you to write and run your own macros.
# You can easily copy and paste commands from the Command History into
# the Macro Script Editor.


# Help
# --------------------------------------------------------------------
# Two documents are available to help you in creating new macros:
#   - Help -> Reference Guides -> Commands (HTML file containing all the available macro commands)
#   - Help -> Reference Guides -> Macro Scripts Reference Guide (PDF file that will take you from
#             creating basic to advanced macro scripts )
#
# Two webinars are also available on our Youtube channel
#   - Customizing the PolyWorks Graphical User Interface (Put a macro in an interface button)
#   - Simplifying tasks using macro scripts

# Additional macro topics are also available on our Youtube channel:
#   - Custom Tools Using the Macro Script Editor
#   - Utilizing PolyWorks Macro Scripting for Lean Process Improvements


# Save & Run
# --------------------------------------------------------------
# Macros can be saved and run from any directory. 
# User Configuration (.innovmetric): Best location if you want to run in from multiple projects
# Workspace (*_Files\macros\): Best location if a macro is only used in one specific project
#
# Check Syntax: Make sure your code doesn't have errors before running it 
#              (Macro Script Editor -> Debug -> Check Syntax)
# Run: Run through a complete macro
#      (Macro Script Editor -> Debug -> Run)
# Step: Step through the macro, allowing you to see and understand what's going on.
#       Recommended for this tutorial (F10 or Macro Script Editor -> Debug -> Run)
#
# Multiple tools are available to debug a macro script:
#   - Break Points will stop the Run command, then resume running or stepping through the macro
#   - Run to cursor, skip, etc.


# Text
# ------------------------------------------------------------
# Version: The Script version is required (start of a script)
# Comments: Use "#" at the start of the line to comment it out


# Commands
# ------------------------------------------------------------
# Commands: Perform actions (written in uppercase).
# Arguments: Give the specific details on the actions to be taken, such as on what object the action should be performed.
# 
# Auto-complete will provide choices when manually entering commands.
# For example in the Workspace Manager:
#    - After typing "W" the auto-complete flyout window will suggest WINDOW, WORKSPACE or WHILE.
#    - After typing WINDOW, you can chose between APPLICATION, REFRESH, etc.
#    - After typing the complete Command WINDOW VIEW, you can fill in the Arguments.

WINDOW VIEW ( "Command History", "On" )


# Echo
# -----------------------------------------------------------
# There are 2 ways to display information to the user:
# MACRO ECHO: Will output information to the Command History
# MACRO PAUSE: Will pop a window with information
# 
# Quotes: Note that Quotes "" are required when using text

MACRO ECHO ( "Hello World." )
MACRO PAUSE ( "Hi", "Hello Earth." )


# Variables
# -------------------------------------------------------------------
# Variables are used to store information (imagine a container, or a bucket).
# You can either put information "IN" the container, or take it "OUT" to use it.
#
# DECLARE: For that container to exist, it needs to be declared first.
# SET: Use this command to assign a value to a variable, once declared. 
#
# You can also set the value of the variables by adding the value after the variable name (optional)
#
# $: Needed if you want to use the value of a variable (OUT)
# {}: Needed to isolate a variable within a string of text
#
# Variables Types (automatically detected, no need to specify):
#   - Integer: Whole number (no decimal point)
#   - Double: Number that allows decimal points
#   - String: List of alphanumeric characters
#
# Variable Modifiers
#   :l Lowercase
#   :u Uppercase
# 
# Reserved Variables
#  - _PI (3.14159...)
#  - Many others starting with underscore "_"
#
# Mouse Over: Note that you can mouse over variables to get their values.


DECLARE variable1 "Message 1"
DECLARE variable2 
DECLARE a 1
DECLARE b

SET variable2 "Message 2"
SET b 2

MACRO ECHO ( $variable2 )
MACRO PAUSE ( "Use Variable", $variable1 )

MACRO ECHO ( "Message = $variable2" )
MACRO PAUSE ( "Followed", "$variable2 followed by extra words" )
MACRO PAUSE ( "Isolate", "${variable2}345 closely followed by extra numbers (345), and then words" )

MACRO PAUSE ( "PI", "Pi = ${_PI}" )
MACRO PAUSE ( "Uppercase", "$variable1 Uppercase = ${variable1:u}" )


# Mathematical Expressions
# -------------------------------------------------------------------------------
# EXPR: Computes an equation to set a value
# EXPR_I: Computes an equation and keeps the integer part of the result (no rounding)
# +, -, *, /, % (Modulo): Arithmetic operators available in equations
# ABS (Absolute), SQRT (Square Root), SIN, COS, TAN, etc. : More operators

DECLARE c
DECLARE d
DECLARE e

SET c EXPR ( $a + $b )
SET d EXPR ( SQRT( $c ) )
SET e EXPR_I ( SQRT( $c ) )

MACRO PAUSE ( "Math", "$a + $b = $c", "Square Root of $c = $d", "Square Root of $c (no decimals) = $e" )


# Logical Expressions
# -------------------------------------------------------------------------------
# You can use logicial expressions (conditions) to have a particular processing done.
#
# IF:     Start the conditional statement 
# ELSEIF: Add alternative conditions
# ELSE:   Indicate an alternative for cases where all IF or ELSEIF conditions are false
# ENDIF:  Stop the conditional statement 
#
# Comparison operators:
#   < smaller than
#   <= smaller than or equal to
#   > larger than
#   >= larger than or equal to
#   == equal to
#   != different from
# 
# Logical operators:
#   AND (the two conditions must be true)
#   OR  (at least one of the two conditions must be true)
#   NOT (inverts the logic)

IF $c == 0
    MACRO PAUSE ( "Zero", "$c equals zero." )
ELSEIF $c < 0
    MACRO PAUSE ( "Smaller than zero", "$c is negative (<0)." )
ELSE
    MACRO PAUSE ( "Bigger than zero", "$c is positive (>0)." )
ENDIF

IF $a > 0 AND $b > 0
    MACRO PAUSE ( "Bigger than zero", "$a AND $b are both bigger than zero." )
ENDIF

IF $a > 0 OR $b > 0
    MACRO PAUSE ( "Bigger than zero", "$a OR $b is bigger than zero." )
ENDIF

# Arrays
# -------------------------------------------------------------------------------
# Multiple values assigned to a single variable is called an array.
# The first value of that array is variable[1] (Second value is variable[2]).
#
# Size: Get the number of values present in the variable array.
# {}: Useful to declare an array

DECLARE PolyWorks { "Inspector", "Modeler", "IMAlign", "IMMerge" }
DECLARE PolyWorksSize SIZE( PolyWorks )
MACRO PAUSE ( "Main modules", "The $PolyWorksSize main modules of PolyWorks are: $polyWorks[1], $polyWorks[2], $polyWorks[3] and $polyWorks[4]" )

# Loops
# -------------------------------------------------------------------------------
# Loops are useful to repeat steps.
#
# WHILE: Start a loop
# ENDWHILE: Stop a loop
# BREAK: End the repeating loop
# CONTINUE: Continue outside of the repeating loop
#
# WHILE loops may use a counter (e.g. "i") to count cycles through the loop.
# Once the counter has reached its indicated value, the loop stops.
#
# ++: Increment variable values (same as: SET i EXPR ( $i + 1 ) )
# --: Decrement variable values (same as: SET i EXPR ( $i - 1 ) )

DECLARE PolyWorksIter 1
WHILE $PolyWorksIter <= $PolyWorksSize
    MACRO ECHO( "PolyWorks Module $PolyWorksIter = $PolyWorks[$PolyWorksIter]" )
    
    ++ PolyWorksIter
ENDWHILE 

# User Input
# --------------------------------
# You can interact with the user to get input.
#
# Question:  Yes/No question (returns 1 for yes or 0 for no)
# Directory: Browse for a Path
# File_Path: Browse for a File
# Double:    Input a Double
# Integer:   Input an Integer
# String:    Input a String
# Multiple:  Input Multiple Parameters (arguments: 1-type, 2-label, 3-default value)
#
# More Variable Modifiers
#   :e Keep the Suffix (Extract file extension)
#   :r Remove the Suffix (Remove file extension)
#   :h Keep File Path (Remove file name)
#   :t Remove File Path (Keep file name)

DECLARE answer
MACRO INPUT QUESTION ( answer, "Click on YES or No" )

IF $answer == 1
    MACRO PAUSE ( "Question", "You clicked: YES" )
ELSE 
    MACRO PAUSE ( "Question", "You clicked: NO" )
ENDIF 

DECLARE fileName
MACRO INPUT FILE_PATH ( fileName, "Browse for a File" )
MACRO PAUSE ( "File", "The FILE is: $fileName", "The file PATH is: $fileName:h", "The file EXTENSION is: $fileName:e", "The file NAME is: $fileName:t:r" )

DECLARE folderName
MACRO INPUT FOLDER_PATH ( folderName, "Select a Folder", )
MACRO PAUSE ( "Folder", "The folder path is: $folderName" )

DECLARE name "John"
DECLARE age "35"
DECLARE height "1.65"
MACRO INPUT MULTIPLE_PARAMETERS ( "Multiple Parameters", "About you:",\
    {"String", "    Name", $name,\
    "Integer", "    Age", $age,\
    "Double", "    Height", $height},\
    name, age, height )
MACRO PAUSE ( "About You", "$name is $age years old (${height}m tall)." )


# Text files
# ---------------------------------------------
# Text files can be written/read. When reading a text file, it may be read one line
# at a time, or all at once and stored in an array for each file column.
#
# More reserved variables:
#   - _TEMP_PATH: Temporary folder (will get deleted upon rebooting)
#   - _PWK_FILES_PATH: Folder inside the Workspace (will travel along with a project)

DECLARE textFileName "${_PWK_FILES_PATH}\user-data\Text_File_Name.txt"
DECLARE textFileFields
DECLARE textFileLineNb
DECLARE textFileLineIter

DATA_FILE CREATE ( $textFileName, "Ascii", "Yes" )
DATA_FILE APPEND LINES ( $textFileName, "John,Lennon" )
DATA_FILE APPEND LINES ( $textFileName, "Paul,McCartney" )
DATA_FILE APPEND LINES ( $textFileName, "Ringo,Starr" )
DATA_FILE APPEND LINES ( $textFileName, "George,Harrison" )

DATA_FILE PROPERTIES NB_LINES GET ( $textFileName, textFileLineNb )

SET textFileLineIter 1
WHILE $textFileLineIter <= $textFileLineNb
    DATA_FILE READ LINE_FIELDS ( $textFileName, $textFileLineIter, textFileFields, ",", "On" )
    
    IF $textFileFields[1] == "Ringo"
        MACRO PAUSE ( "Data File", "$textFileFields[1] is a ${textFileFields[2]}!" )
        BREAK
    ENDIF
    
    ++ textFileLineIter
ENDWHILE


DECLARE firstName
DECLARE lastName
SET textFileLineIter 1

DATA_FILE READ COLUMNS ( "${_PWK_FILES_PATH}\user-data\Text_File_Name.txt", ",", "Off", 1, 4, firstName, lastName )
DATA_FILE CREATE ( "${_PWK_FILES_PATH}\user-data\Text_file_paul_only.txt", , )
WHILE $textFileLineIter <= 4
    IF $firstName[$textFileLineIter] == "Paul"
        DATA_FILE APPEND ( "${_PWK_FILES_PATH}\user-data\Text_file_paul_only.txt", "$firstName[$textFileLineIter] $lastName[$textFileLineIter]", )
    ENDIF
    ++ textFileLineIter
ENDWHILE

```
