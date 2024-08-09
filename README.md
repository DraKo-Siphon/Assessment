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


# Function to check the length
def check_length(name):
    return len(name) <= 20

# Function to check the presence
def check_presence(name):
    return name != ""

# Function to check if the input contains only alphabets
def check_text(name):
    return name.isalpha()

# Function to validate the input
def validate_input():
    def print_receipt(receipt_number, first_name, last_name, item, quantity):
        view_receipt = tk.Toplevel()
        view_receipt.title("Receipt")
        view_receipt.configure(bg=dark_blue)

# Function to check if quantity is between 1 and 500
def check_quantity(quantity):
    try:
        qty = int(quantity)
        return 1 <= qty <= 500
    except ValueError:
        return False

        receipt_frame = tk.LabelFrame(view_receipt, text="Receipt", bg=light_blue, fg=white, font=('Helvetica', 14, 'bold'))
        receipt_frame.grid(row=0, column=0, padx=20, pady=10)

        tk.Label(receipt_frame, text=f"Receipt Number: {receipt_number}", bg=light_blue, fg=white).pack(pady=5)
        tk.Label(receipt_frame, text=f"First Name: {first_name}", bg=light_blue, fg=white).pack(pady=5)
        tk.Label(receipt_frame, text=f"Last Name: {last_name}", bg=light_blue, fg=white).pack(pady=5)
        tk.Label(receipt_frame, text=f"Item: {item}", bg=light_blue, fg=white).pack(pady=5)
        tk.Label(receipt_frame, text=f"Quantity: {quantity}", bg=light_blue, fg=white).pack(pady=5)

    # Get the input values
    first_name = first_name_entry.get().strip()
    last_name = last_name_entry.get().strip()
    item = item_combobox.get().strip()
    quantity = quantity_spinbox.get().strip()
    receipt_number = generate_receipt_number()

    # Debugging 
    print(f"Debug: First Name: '{first_name}'")
    print(f"Debug: Last Name: '{last_name}'")
    print(f"Debug: Item: '{item}'")
    print(f"Debug: Quantity: '{quantity}'")

    # Validation
    if not check_presence(first_name):
        messagebox.showerror("Error in Input", "First name cannot be blank.")
    elif not check_length(first_name):
        messagebox.showerror("Error in Input", "First name must be shorter than 20 characters.")
    elif not check_text(first_name):
        messagebox.showerror("Error in Input", "First name must contain only alphabets.")
    elif not check_presence(last_name):
        messagebox.showerror("Error in Input", "Last name cannot be blank.")
    elif not check_length(last_name):
        messagebox.showerror("Error in Input", "Last name must be shorter than 20 characters.")
    elif not check_text(last_name):
        messagebox.showerror("Error in Input", "Last name must contain only alphabets.")
    elif not check_presence(item):
        messagebox.showerror("Error in Input", "Item cannot be blank.")
    elif item not in ["Chairs", "Tables", "Candles", "Confetti"]:
        messagebox.showerror("Error in Input", "Item must be from the list provided.")
    elif not check_quantity(quantity):
        messagebox.showerror("Error in Input", "Quantity must be a number between 1 and 500.")
    else:
        user_entries.append({
            "first_name": first_name,
            "last_name": last_name,
            "item": item,
            "receipt_number": receipt_number,
            "quantity": quantity
        })
        with open("user_entries.txt", "a") as file:
            file.write(f"{first_name},{last_name},{item},{receipt_number},{quantity}\n")
        
        response = messagebox.askyesno("Entry Complete", f"Entry is stored with Receipt Number: {receipt_number}. Do you want to return to the main window?")
        if response:
            print_receipt(receipt_number, first_name, last_name, item, quantity)
first_name_entry.get_toplevel().destroy()
        else:
            exit()

# This is the Refund Window
def refund_window():
    global refund_first_name_entry, refund_last_name_entry, refund_receipt_entry, refund_quantity_label, refund_quantity_spinbox

    refund = tk.Toplevel()
    refund.title("Refund Window")
    refund.configure(bg=dark_green) 

    refund_frame = tk.LabelFrame(refund, text="Refund Details", bg=light_green, font=custom_font)
    refund_frame.grid(row=0, column=0)

    refund_first_name_label = tk.Label(refund_frame, text="First Name", bg=light_green, font=custom_font)
    refund_first_name_label.grid(row=0, column=0, padx=20, pady=10)
    refund_first_name_entry = tk.Entry(refund_frame, font=custom_font, bg=white)
    refund_first_name_entry.grid(row=1, column=0, padx=20, pady=10)

    refund_last_name_label = tk.Label(refund_frame, text="Last Name", bg=light_green, font=custom_font)
    refund_last_name_label.grid(row=0, column=1, padx=20, pady=10)
    refund_last_name_entry = tk.Entry(refund_frame, font=custom_font, bg=white)
    refund_last_name_entry.grid(row=1, column=1, padx=20, pady=10)

    refund_quantity_label = tk.Label(refund_frame, text="Quantity", bg=light_green, font=custom_font)
    refund_quantity_spinbox = tk.Spinbox(refund_frame, from_=1, to=500, font=custom_font)
    refund_quantity_label.grid(row=2, column=1, padx=20, pady=10)
    refund_quantity_spinbox.grid(row=3, column=1, padx=20, pady=10)

    refund_receipt_label = tk.Label(refund_frame, text="Receipt Number", bg=light_green, font=custom_font)
    refund_receipt_label.grid(row=2, column=0, padx=20, pady=10)
    refund_receipt_entry = tk.Entry(refund_frame, font=custom_font, bg=white)
    refund_receipt_entry.grid(row=3, column=0, padx=20, pady=10)

    refund_item_label = tk.Label(refund_frame, text="Item", bg=light_green, font=custom_font)
    refund_item_combobox = ttk.Combobox(refund_frame, values=["Chairs", "Tables", "Candles", "Confetti"], font=custom_font)
    refund_item_label.grid(row=0, column=2, padx=20, pady=10)
    refund_item_combobox.grid(row=1, column=2, padx=20, pady=10)

    refund_button = tk.Button(refund_frame, text="Submit", command=process_refund, font=custom_font, bg=light_green, fg=white)
    refund_button.grid(row=4, column=0)

    back_button = tk.Button(refund_frame, text="Back to Main", command=refund.destroy, font=custom_font, bg=light_green, fg=white)
    back_button.grid(row=4, column=1, padx=10, pady=5)

# Function to process the refund
def process_refund():
    first_name = refund_first_name_entry.get().strip()
    last_name = refund_last_name_entry.get().strip()
    receipt_number = refund_receipt_entry.get().strip()
    refund_quantity = int(refund_quantity_spinbox.get().strip())

    for entry in user_entries:
        if entry["receipt_number"] == receipt_number:
            current_quantity = int(entry["quantity"])
            if refund_quantity >= current_quantity:
                user_entries.remove(entry)
            else:
                entry["quantity"] = str(current_quantity - refund_quantity)
            with open("user_entries.txt", "w") as file:
                for entry in user_entries:
                    file.write(f"{entry['first_name']},{entry['last_name']},{entry['item']},{entry['receipt_number']},{entry['quantity']}\n")
            messagebox.showinfo("Refund Processed", f"Refund processed for Receipt Number: {receipt_number}")
            return

    messagebox.showerror("Refund Error", "Receipt Number not found.")

def load_receipts():
    global user_entries
    try:
        with open("user_entries.txt", "r") as file:
            for line in file:
                first_name, last_name, item, receipt_number, quantity = line.strip().split(",")
                user_entries.append({
                    "first_name": first_name,
                    "last_name": last_name,
                    "item": item,
                    "receipt_number": receipt_number,
                    "quantity": quantity
                })
    except FileNotFoundError:
        pass

# This is the View Receipts Window
def view_receipts_window():
    view_receipts = tk.Toplevel()
    view_receipts.title("View Receipts")
    view_receipts.configure(bg=dark_green) 

    view_frame = tk.Frame(view_receipts, bg=dark_green)
    view_frame.pack(padx=20, pady=20)

    if user_entries:
        for entry in user_entries:
            receipt_info = (f"Receipt Number: {entry['receipt_number']} - Name: {entry['first_name']} {entry['last_name']} "
                            f"- Item: {entry['item']} - Quantity: {entry['quantity']}")
            tk.Label(view_frame, text=receipt_info, bg=dark_green, fg=white, font=custom_font).pack(pady=5)
    else:
        tk.Label(view_frame, text="No receipts available", bg=dark_green, fg=white, font=custom_font).pack(pady=5)

    back_button = tk.Button(view_frame, text="Back to Main", command=view_receipts.destroy, font=custom_font, bg=light_green, fg=white)
    back_button.pack(pady=10)

    try:
        with open("user_entries.txt", "r") as file:
            lines = file.readlines()
            if not lines:
                view_receipts_listbox.insert(tk.END, "There were no receipts found.")
                return

            for line in lines:
                line = line.strip()
                if line:  # Check if line is not empty
                    parts = line.split(",")
                    if len(parts) == 5:  # Ensure there are exactly 5 parts
                        first_name, last_name, item, receipt_number, quantity = parts
                        receipt_display = (f"Receipt Number: {receipt_number} | Name: {first_name} {last_name} "
                                           f"| Item: {item} | Quantity: {quantity}")
                        view_receipts_listbox.insert(tk.END, receipt_display)
                    else:
                        view_receipts_listbox.insert(tk.END, f"Incorrect line: {line}")
    except FileNotFoundError:
        view_receipts_listbox.insert(tk.END, "Receipts file not found.")
# Function to confirm quit

def confirm_quit():
    if messagebox.askokcancel("Quit", "Do you want to quit?"):
        main_window.destroy()

# Start the main window
if __name__ == "__main__":
    main_window()



