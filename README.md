import tkinter as tk
from tkinter import messagebox

class CalculatorApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Simple Calculator")

        self.result_var = tk.StringVar()

        self.create_widgets()

    def create_widgets(self):
        # Result display
        result_entry = tk.Entry(self.root, textvariable=self.result_var, font=("Arial", 20), bd=10, insertwidth=2, width=14, borderwidth=4)
        result_entry.grid(row=0, column=0, columnspan=4)

        # Buttons
        buttons = [
            '7', '8', '9', '/', 
            '4', '5', '6', '*', 
            '1', '2', '3', '-', 
            '0', '.', '=', '+'
        ]

        row = 1
        col = 0
        for button in buttons:
            tk.Button(self.root, text=button, padx=20, pady=20, font=("Arial", 20),
                      command=lambda b=button: self.on_button_click(b)).grid(row=row, column=col)
            col += 1
            if col > 3:
                col = 0
                row += 1

    def on_button_click(self, button):
        current_text = self.result_var.get()
        
        if button == "=":
            try:
                result = str(eval(current_text))
                self.result_var.set(result)
            except Exception as e:
                messagebox.showerror("Error", "Invalid Input")
                self.result_var.set("")
        elif button == "C":
            self.result_var.set("")
        else:
            new_text = current_text + button
            self.result_var.set(new_text)

if __name__ == "__main__":
    root = tk.Tk()
    app = CalculatorApp(root)
    root.mainloop()
