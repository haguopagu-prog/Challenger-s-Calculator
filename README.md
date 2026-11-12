Python

import tkinter as tk
import math

root = tk.Tk()
root.title("Scientific Calculator")
root.geometry("350x450")
root.configure(bg="#222222")

display = tk.Entry(
    root, font=("Arial", 22),
    justify="right"
)
display.pack(fill="x", padx=10, pady=10)

def calculate(value):
    if value == "C":
        display.delete(0, tk.END)

    elif value == "=":
        try:
            expression = display.get()
            result = eval(expression, {"__builtins__": {}},
                          {"sqrt": math.sqrt,
                           "sin": math.sin,
                           "cos": math.cos,
                           "tan": math.tan,
                           "log": math.log10,
                           "pi": math.pi,
                           "e": math.e})
            display.delete(0, tk.END)
            display.insert(tk.END, str(result))
        except:
            display.delete(0, tk.END)
            display.insert(tk.END, "Error")

    else:
        display.insert(tk.END, value)

buttons = [
    ["7", "8", "9", "/"],
    ["4", "5", "6", "*"],
    ["1", "2", "3", "-"],
    ["0", ".", "(", ")"],
    ["sin(", "cos(", "tan(", "+"],
    ["sqrt(", "log(", "pi", "="],
    ["C"]
]

for row in buttons:
    frame = tk.Frame(root, bg="#222222")
    frame.pack()

    for text in row:
        tk.Button(
            frame,
            text=text,
            width=7,
            height=2,
            font=("Arial", 12),
            command=lambda x=text: calculate(x)
        ).pack(side="left", padx=2, pady=2)

root.mainloop()
