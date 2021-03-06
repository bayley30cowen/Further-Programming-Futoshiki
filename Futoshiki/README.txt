/***********************************************
*******************README FILE******************
*************FOR FUTOSHIKI ASSIGNMENT 3*********
******************CREATED BY 184514*************
***********************************************/
//How the actually GUI works

1. When the GUI starts, the user is prompted to
enter a size of the puzzle they wish to play with
and the difficulty they wish to play on. I have 
chosen to do it this way, as some users may want
to choose their difficulty and size straight away
and not want to have a randomly generated board
with a size they may not like, or a difficulty 
too hard.
2. If the user wants to change the size/difficulty
of the grid, go to tab labelled new game, and choose
a new size or a new difficulty. User is then prompted
to enter new value for difficulty/size and new grid is
created. for some reason, you must change the size of the grid 
before changing difficulty
as if you try to change difficulty first the program crashes. 
I have looked over this multiple times and cannot find why this is happening.
3. Un-editable tiles have the number within the cell in white
and the background of the cell in grey. The state of editable tiles
is that if the background is white it is editable.
4. When marking a tile, the user must enter a number between 1 and
the size of the grid i.e. if it is a 5x5, the highest number
that can be entered is 5. If a number is entered that is not
valid the user is notified and the value is NOT entered into
the square. this is done through a Message box. If the user does not
want to enter a value they can simply click off of the square.
5. When the puzzle is complete and the final state IS legal, the user
will click on check puzzle button. if the puzzle is valid, but has empty squares,
no alert box is given to the user. If the puzzle is valid and has no empty squares
a congratulation message is sent to the user. the code will then generate a new 
puzzle for the user to complete.
6. If the user chooses to give up, they can click the give up button
this will close the game. I have added a confirm box here incase the user accidently
clicks give up. This means that they must confirm that they wish to give up.
7. If the user cant work out the complete result, they can chose to solve the grid for them
this is done by clicking the button solve me! again this has a confirm box incase it was clicked accidently.
The solve algorithm uses dfs to determine whether it is finish able, so only legal finish able grids are
created. A DFS algorithm is used to see if the puzzle is solvable, and is used before displaying the grid
to the user to ensure so only finish able grids are created from fill Puzzle method.

//How the code works

Displaying the data:
--------------------
Uses nested loops to check one cell of all three arrays at a time.
If a value is the initial value, this means it was generated by the fillPuzzle method
and has been checked to be legal. This makes this value correct and legal, so these 
squares will be uneditable. The code sets the colour of the font of uneditable squares
to white and the background to grey.  If the square is editable, the background is
white with black font.

getValue is the method used to fetch the values from the FutoshikiGrid object
 
Since the constraints will always be uneditable, they will always look the same
If the getValue for getSquare returns 0, i.e. no value, " " is printed in the label of the square to show
that the square is editable.

The grid uses a JFrame function, setPreferedSize which is able to scale the puzzle
to ensure it always fits in the same window. This means a 5x5 puzzle will fit in the same
space a 10x10 could. 

The board stays upto date due to the use  of calling startGame, which ensures that the 
data being displayed in the grid is the most recent/data being stored in the futoshiki
grid object.

The GUI is able to display the solve method, by solving the puzzle using the DFS 
method, and storing the last found legal puzzle solution into the grid, which is the updated
in the GUI by calling the startGame() method.

Editing data:
--------------
The board allows for data to be entered due the use of a key listener. When a value is entered 
into a square, the keyListener checks it a valid value, and if it is allows for it to be entered
into the grid, by calling the startGame method. If the number/value entered is invalid
the grid does not store the number, and the user is alerted to this.
Once the value entered is confirmed to be legal i.e. not out of bounds, it is added to the panel
and then the panel is added to the futoshikiGrid. 


Optional Features:
------------------
	Saving the grid: 
------------------------
Sets the file output stream and object output stream to nothing/null. Uses a try, catch
to create a file output stream and object output stream, if a file is found. Then writes
the grid as an object to the file, and closes the file. If no file is found, method prints a stack 
trace for this Throwable object on the standard error output stream.
I found this feature would be good, if the user wants to save a particular part of the 
grid to try a way of solving, but is scared of losing progress, so can save the file at a checkpoint
and load it back if they want to start again from  that checkpoint.
------------------------	
	Loading the grid:
------------------------
Uses the readObejct method, to read the filename suppiled and store the result in the
futoshikiGrid display. If no file is found, method prints a stack trace for this 
Throwable object on the standard error output stream.
This feature comes with the save feature, as there is no point of being able to save a file, without being able to use that save, 
by loading it back in.
------------------------
	Displays problems with grid to user:
------------------------
To display the problems with the grid, using the function getAllProbelms(), in the check
puzzle code, if the puzzle is not legal, using the checkIfLegal() function, the function
sets the text, using setText() function for a Text Area, the string of problems is printed to
the user. I found this would be very helpful as now the user knows whats wrong
with the grid and is able to easily fix the mistakes.
------------------------
	Allowing user to choose starting size
------------------------
From what I have experienced, if a random size is given to the user, it could lead to
longer load times. By allowing the user to choose a size from the beginning loads times
are shorter, and the user will not need to change the size in the features menu bar
as they are happy with the starting size, since they chose it.
To implement this, A panel, with just a textfield is displayed to the user
The panel only has a label asking for the user to input a starting size. Once the user
has entered a valid value into the textfield, the window closes and a futoshikiGrid
of their chosen size opens. The getText() function is used to get the value entered and
parseInt() method is used to convert the string into an int, which is the stored as 
the size of the puzzles. This is only updated when the user wants to play on a board of a different size
An action listener is used, to listen for when the enter button is clicked, so the value
entered by the user can be stored. If the value entered is not an int, or is out of range,
user is alerted and is asked to re-enter.
