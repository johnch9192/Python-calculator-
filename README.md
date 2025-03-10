# Python-calculator-
import tkinter as tk
from math import sqrt

def click(event):
    text = event.widget.cget("text")
    current_text = entry_var.get()

    if text == "=":
        try:
            result = eval(current_text)  # Evaluate the mathematical expression
            entry_var.set(result)
        except Exception:
            entry_var.set("Error")
    elif text == "C":
        entry_var.set("")
    elif text == "√":
        try:
            result = sqrt(float(current_text))
            entry_var.set(result)
        except:
            entry_var.set("Error")
    elif text == "^":
        entry_var.set(current_text + "**")  # Convert "^" to "**" for exponentiation
    elif text == "Exit":
        root.destroy()  # Close the calculator
    else:
        entry_var.set(current_text + text)  # Append clicked button text

# Create main window
root = tk.Tk()
root.title("Calculator")
root.geometry("300x400")
root.configure(bg="lightgray")

entry_var = tk.StringVar()
entry = tk.Entry(root, textvar=entry_var, font="Arial 20 bold", justify="right", bd=10)
entry.pack(fill="both", ipadx=8, pady=10, padx=10)

# Buttons
buttons = [
    ["7", "8", "9", "/"],  # Division
    ["4", "5", "6", "*"],  # Multiplication
    ["1", "2", "3", "-"],  # Subtraction
    ["C", "0", "=", "+"],  # Addition & Clear
    ["√", "^", ".", "Exit"]  # Square root, Exponent, Decimal, Exit
]

frame = tk.Frame(root)
frame.pack()

for row in buttons:
    btn_row = tk.Frame(frame)
    btn_row.pack(side="top", fill="both", expand=True)
    for btn_text in row:
        button = tk.Button(btn_row, text=btn_text, font="Arial 18 bold", height=2, width=5, relief="ridge")
        button.pack(side="left", fill="both", expand=True)
        button.bind("<Button-1>", click)  # Bind all buttons inside the loop

# Run the Tkinter event loop
root.mainloop()
