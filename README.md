# Assessment
import tkinter as tk
from tkinter import ttk, messagebox
import random
import string


# List to store the user entries
user_entries = []

# Define a custom font
custom_font = ("Helvetica", "16")

# Define colors
dark_green = '#0c67c2'
light_green = '#9bbdde'
white = '#ffffff'

#This is the Main Window
def main_window():
    global main_window
    main_window = tk.Tk()
    main_window.title("Julie's Party Hire")
    main_window.configure(bg=dark_green)

    main_frame = tk.Frame(main_window, bg=dark_green)
    main_frame.pack(padx=20, pady=20)

    #Image

    # Hire button
    hire_button = tk.Button(main_frame, text="Hire Item", command=hire_window, font=custom_font, bg=light_green, fg=white, width=12)
    hire_button.grid(row=1, column=1, padx=20, pady=10)

    # Refund Button
    return_button = tk.Button(main_frame, text="Refund", command=refund_window, font=custom_font, bg=light_green, fg=white, width=12)
    return_button.grid(row=2, column=1, padx=2, pady=10)

    # View Receipts Button
    view_receipts_button = tk.Button(main_frame, text="View Receipts", command=view_receipts_window, font=custom_font, bg=light_green, fg=white, width=12)
    view_receipts_button.grid(row=3, column=1, padx=2, pady=10)

    # Quit Button
    quit_button = tk.Button(main_frame, text="Quit", command=confirm_quit, font=custom_font, bg=light_green, fg=white, width=12)
    quit_button.grid(row=4, column=1, padx=20, pady=10)

    main_window.mainloop()

# This is the Hire Window 
def hire_window():
    global receipt_label, first_name_entry, last_name_entry, item_combobox, quantity_spinbox, two_functions

    # Hire Window Itself
    hire = tk.Toplevel()
    hire.title("Hire Window")
    hire.configure(bg=dark_green)  

    # Hire Window Frame
    hire_frame = tk.LabelFrame(hire, text="Hire Item Details", bg=light_green, font=custom_font)
    hire_frame.grid(row=0, column=0)

    # First & Last Name Input
    first_name_label = tk.Label(hire_frame, text="First Name", bg=light_green, font=custom_font)
    first_name_label.grid(row=0, column=0, padx=20, pady=10)              
    first_name_entry = tk.Entry(hire_frame, font=custom_font, bg=white) 
    first_name_entry.grid(row=1, column=0, padx=20, pady=10)

    last_name_label = tk.Label(hire_frame, text="Last Name", bg=light_green, font=custom_font)
    last_name_label.grid(row=0, column=1, padx=20, pady=10)
    last_name_entry = tk.Entry(hire_frame, font=custom_font, bg=white) 
    last_name_entry.grid(row=1, column=1)

    # Item Input
    item_label = tk.Label(hire_frame, text="Item", bg=light_green, font=custom_font)
    item_combobox = ttk.Combobox(hire_frame, values=["Chairs", "Tables", "Candles", "Confetti"], font=custom_font)
    item_label.grid(row=0, column=2, padx=20, pady=10)
    item_combobox.grid(row=1, column=2, padx=20, pady=10)

    # Quantity Input
    quantity_label = tk.Label(hire_frame, text="Quantity", bg=light_green, font=custom_font)
    quantity_spinbox = tk.Spinbox(hire_frame, from_=1, to=500, font=custom_font)
    quantity_label.grid(row=2, column=1, padx=20, pady=10)
    quantity_spinbox.grid(row=3, column=1, padx=20, pady=10)

    # Submit & Back Button
    validate_button = tk.Button(hire_frame, text="Submit", command=validate_input, bg=light_green, font=custom_font, fg=white)
    validate_button.grid(row=4, column=1)

    back_button = tk.Button(hire_frame, text="Back to Main", command=hire.destroy, font=custom_font, bg=light_green, fg=white)
    back_button.grid(row=4, column=0, padx=10, pady=5)

# Function to generate a random receipt number
def generate_receipt_number():
    receipt_number = ''.join(random.choices(string.ascii_uppercase + string.digits, k=3))
    existing_receipt_numbers = [entry["receipt_number"] for entry in user_entries]
    while receipt_number in existing_receipt_numbers:
        receipt_number = ''.join(random.choices(string.ascii_uppercase + string.digits, k=3))
    return receipt_number
