# Truffula Notes
As part of Wave 0, please fill out notes for each of the below files. They are in the order I recommend you go through them. A few bullet points for each file is enough. You don't need to have a perfect understanding of everything, but you should work to gain an idea of how the project is structured and what you'll need to implement. Note that there are programming techniques used here that we have not covered in class! You will need to do some light research around things like enums and and `java.io.File`.

PLEASE MAKE FREQUENT COMMITS AS YOU FILL OUT THIS FILE.

## App.java
- Inside of this class is the main method that calls the TruffulaOptions object, which can have flags passed as arguments that manipulate the behavior of the printed directory tree (order of flags ignored)
- Although the TruffulaOptions object only requires one argument: the path to the directory which contents are to be printed
- \['\-nc', '\-h', '/path/to/directory' \]
- \-nc (no color) \-h (show hidden files)
## ConsoleColor.java
- This is an enum which holds constant values of colors and their corresponding ANSI code
- Used to be able to predictably dictate what color your printed directory tree text is (in supported terminals)
- To use, one must prepend the ANSI code to the text, or append the RESET code to reset back to black 
## ColorPrinter.java / ColorPrinterTest.java
- ColorPrinter is a helper class for printing colored text to a PrintStream using ANSI escape codes 
- ColorPrinter allows setting a current color and then printing messages in that specified color
- Caveat: Colors can be reset after each print or kept active based on the provided parameters
- ColorPrinter can only understand ANSI codes defined in the enum class ConsoleColor.java
- ColorPrinterTest is a testing class which is used to verify the validity of the code in ColorPrinter, where it attempts to capture the printed output, print the message, and then verify if the printed output is as suggested
## TruffulaOptions.java / TruffulaOptionsTest.java
- TruffulaOptions represents the configuration options for controlling how the directory tree is displayed.
- Three arguments are allowed, (\-h, \-nc, /path/to/directory), but only the path is required
- Throws an IllegalArgumentException if unknown flags are provided or if the path arg is missing, or a FileNotFoundException if the path does not exist, or points to a file instead of a directory.
- TruffulaOptionsTest, tests the validity of TruffulaOptions, by creating a temporary directory, and test options, where the properties of TruffulaOptions are checked to confirm they are as provided.
## TruffulaPrinter.java / TruffulaPrinterTest.java
- Question: I thought that ColorPrinter was responsible for printing a tree structure with color?
- TruffulaPrinter is responsible for printing a directory tree structure with an optional colored ouput, supporting sorting files and directories.
- Directories and files are sorted in a case-insensitive manner, with 3 spaces of indentation separating each directory level, with the final expected behavior sorting identical case-insensitive names lexicographically
- TruffulaPrinterTest ensures the sanctity of the code contained within TruffulaPrinter.
- I'm noticing it first checks the operating system, as it seems that windows requires some more specific information about the path, and some file attributes?
## AlphabeticalFileSorter.java
- AlphabeticalFileSorter is a helper class which take in an array of files and sorts them alphabetically
- the method sort(File\[\] files) uses an Arrays.sort() method that I'm pretty sure is the lambda (an anonymous function)
-Files are sorted ignoring case differences, meaning that files with the same name, and only lexiographical differences, will be sorted based on the order they are iterated over.