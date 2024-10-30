import tkinter as tk
import random

# Initialize the main window
root = tk.Tk()
root.title("Compact Slot Machine")
root.geometry("400x600")
root.configure(bg="white")

# Symbols for the slot machine (10 different symbols)
symbols = ["🍒", "⬛", "💲", "🏆", "🌲", "🍋", "💎", "🎲", "🎩", "⭐"]

# Winning options
winning_combinations = {
    "🍒🍒🍒🍒🍒": "Jackpot! You Win!",
    "💎💎💎💎💎": "Diamond Win! You Win!",
    "🏆🏆🏆🏆🏆": "Gold Trophy! You Win!",
    "💲💲💲💲💲": "Money Win! You Win!"
}

# Token variables
tokens = 5

# Slot Labels (5 slots)
slot_labels = []

# Function to check for winning combinations
def check_win():
    current_symbols = "".join([slot.cget("text") for slot in slot_labels])
    if current_symbols in winning_combinations:
        result_label.config(text=winning_combinations[current_symbols], fg="green")
    else:
        result_label.config(text="Try Again!", fg="red")

# Function to "spin" the slots
def spin_slots():
    global tokens
    if tokens > 0:
        # Deduct one token per spin
        tokens -= 1
        update_token_display()
        
        # Randomly assign symbols to each slot
        for slot in slot_labels:
            slot.config(text=random.choice(symbols))
        
        # Check for any winning combination
        check_win()
    else:
        result_label.config(text="Out of Tokens!", fg="red")

# Lever position and dragging variables
lever_y_start = 300
lever_y_end = 400
is_dragging = False

# Function to start dragging the lever
def start_drag(event):
    global is_dragging
    is_dragging = True

# Function to drag the lever
def drag_lever(event):
    if is_dragging:
        # Restrict the lever to only move within the defined range
        new_y = max(lever_y_start, min(event.y, lever_y_end))
        slot_frame.coords(lever, 360, new_y, 380, new_y + 50)

# Function to release the lever and trigger slot spin
def release_lever(event):
    global is_dragging
    if is_dragging:
        is_dragging = False
        current_y = slot_frame.coords(lever)[1]  # Get the current y position of the lever

        # Check if lever was pulled to the bottom before releasing
        if current_y >= lever_y_end - 10:
            spin_slots()  # Spin slots if lever is fully pulled
        # Reset the lever to the starting position
        slot_frame.coords(lever, 360, lever_y_start, 380, lever_y_start + 50)

# Create the token system
def add_token():
    global tokens
    tokens += 1
    update_token_display()

# Update the token display label
def update_token_display():
    token_display.config(text=f"Tokens: {tokens}")

# Create a frame for the slot machine design
slot_frame = tk.Canvas(root, width=400, height=400, bg="white", highlightthickness=0)
slot_frame.pack()

# Draw the slot machine box
slot_frame.create_rectangle(50, 50, 350, 300, outline="black", width=4)  # Slot machine box

# Create slots (5 slots)
for i in range(5):
    slot_label = tk.Label(root, text="", font=("Helvetica", 30), width=3, bg="lightgray")
    slot_label.place(x=60 + i*60, y=150)
    slot_labels.append(slot_label)

# Display the result of the spin
result_label = tk.Label(root, text="", font=("Helvetica", 18), fg="red", bg="white")
result_label.pack(pady=10)

# Token button to add tokens
token_button = tk.Button(root, text="Add Token", command=add_token, bg="gold", font=("Helvetica", 14))
token_button.pack(pady=5)

# Token display label
token_display = tk.Label(root, text=f"Tokens: {tokens}", font=("Helvetica", 16), bg="white")
token_display.pack(pady=5)

# Create the lever on the side of the slot machine
lever = slot_frame.create_rectangle(360, lever_y_start, 380, lever_y_start + 50, fill="orange", outline="black", width=2)

# Bind mouse events to the lever for dragging
slot_frame.tag_bind(lever, "<Button-1>", start_drag)
slot_frame.bind("<B1-Motion>", drag_lever)
slot_frame.bind("<ButtonRelease-1>", release_lever)

# Run the tkinter loop
root.mainloop()
