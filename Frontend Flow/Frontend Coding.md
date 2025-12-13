# JS Calculator
## Algorithm: Simple Calculator

---

### Step 1

Start the program.

---

### Step 2

Display a calculator interface with:

- A display box
    
- Number buttons (0–9)
    
- Operator buttons (+, −, ×, ÷)
    
- Clear button (C)
    
- Equal button (=)
    

---

### Step 3

When a **number or operator button** is clicked:

- Take the value of the button
    
- Append it to the display
    

---

### Step 4

When the **Clear (C) button** is clicked:

- Remove all values from the display
    
- Make the display empty
    

---

### Step 5

When the **Equal (=) button** is clicked:

- Read the expression from the display
    
- Evaluate the mathematical expression
    

---

### Step 6

If the expression is **valid**:

- Show the calculated result in the display
    

---

### Step 7

If the expression is **invalid**:

- Show an error message saying  
    **"Invalid Calculation"**
    

---

### Step 8

Stop the program.

Nice choice of example 👍 This is a clean beginner-friendly calculator, so the pseudocode can also stay simple and clear.

Below is **structured pseudocode** that explains the logic of the JavaScript part step by step.

---

## Pseudocode for Calculator Logic

---

### START

---

### FUNCTION `appendValue(value)`

```
GET the display input field
ADD the given value to the current display value
```

---

### FUNCTION `clearDisplay()`

```
GET the display input field
SET the display value to empty
```

---

### FUNCTION `calculate()`

```
TRY
    GET the expression from the display
    EVALUATE the expression
    SHOW the result in the display
CATCH error
    SHOW message "Invalid Calculation"
END TRY
```

---

### BUTTON BEHAVIOR

```
WHEN a number button is clicked
    CALL appendValue(number)

WHEN an operator button (+, -, *, /) is clicked
    CALL appendValue(operator)

WHEN the C button is clicked
    CALL clearDisplay()

WHEN the = button is clicked
    CALL calculate()
```

---

### END

---

