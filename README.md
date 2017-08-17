ButtonApi

This is a computercraft button api. Coded in OOP fashion.

Creates easy way of managing clickable buttons on advanced monitors in computercraft

### Basic usage:

 1. include api in your file by `os.loadAPI("button")`  
 2. set monitor you want to use: `button.setMonitor(handle)`  
 3. Create button: `myButton = button.create("My new button")`  
 4. Set position: `myButton.setPos(1,1)`  
 5. Set some callback: `myButton.onClick(function() print("CLICK!") end)`  
 6. Setup loop waiting for input: `while true do button.await(myButton) end`  
 And you're done! Once button will be clicked, "CLICK!" will be printed onto computer's term.  
 
### Button object method list
- `setText(text, resize)` - sets button label, if resize=true, recalculates button width
- `setAlign(align)` - sets label align in button; align can be: "left", "right", "center"
- `setPos(x, y)` - sets button's position on screem
- `setSize(width, height)` - sets button's size
- `setColor(color)` - sets background color (from computercraft colors api)
- `setBlinkColor(color)` - sets backgroundColor when button is clicked
- `setActive(state)` - activates/deactivates button; state - boolean
- `onClick(callback)` - sets callback executed when button is pressed
- `onClickReturn(value)` - sets value that will be returned by `button.await` istead of callback function

Adidtionally, all above methods return button object so they can be chained eg:  
`myButton = button.create().setText("Label").setSize(10,1).setPos(2,2).setColor(colors.red)`  

### Other api methods
- `button.create(text)` - returns new button object; `text` parameter is optional
- `button.setMonitor(handle)` - sets handle to connected advanced monitor. (Handle is peripheral.wrap())
- `button.await(button, button1, ...)` - draws given buttons and awaits for monitor click. After click, ends execution, regardless if click hit any button.  
Buttons can be supplied one after:  
`button.await(button1, button2, button3, ...)`  
Or in form of a table:  
```
buttonTable = {button1, button2, button3}
button.await(buttonTable)
```
Or mixed:  
```
buttonTable = {button1, button2, button3}
button.await(buttonTable, button4, button5)
```
Note: In all examples above `button1, button2, etc` means button objects  
If some button was clicked:  
- returns value set by `onClickReturn` on clicked button or
- executes function set by `onClick` method on clicked button
