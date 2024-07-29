# Assessment
import tkinter as tk
from tkinter import ttk, messagebox
import random
import string


# List to store the user entries
user_entries = []

# Define a custom font
custom_font = ("Helvetica", "16")

# This is the home page of the program
def main_window():
    global main_window
    main_window = tk.Tk()
    main_window.title("Julie's Party Hire")
    main_window.configure(bg='green')
    image_path = "images.png"
    back = PhotoImage(file=image_path)
    label = ttk.Label(main_frame, image=photo_image)
    main_frame = tk.Frame(main_window, bg='green')
    main_frame.pack(padx=20, pady=20)

    # Hire button
    hire_button = tk.Button(main_frame, text="Hire Item", command=hire_window, font=custom_font, bg='lightgreen')
    hire_button.grid(row=1, column=1, padx=20, pady=10)

    # Refund Button
    return_button = tk.Button(main_frame, text="Refund", command=refund_window, font=custom_font, bg='lightgreen')
    return_button.grid(row=2, column=1, padx=2, pady=10)

    # View Receipts Button
    view_receipts_button = tk.Button(main_frame, text="View Receipts", command=view_receipts_window, font=custom_font, bg='lightgreen')
    view_receipts_button.grid(row=3, column=1, padx=2, pady=10)

    # Quit Button
    quit_button = tk.Button(main_frame, text="Quit", command=confirm_quit, font=custom_font, bg='lightgreen')
    quit_button.grid(row=4, column=1, padx=20, pady=10)
