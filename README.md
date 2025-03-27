# BINGO BOARD Generator 
import random
import tkinter as tk
from tkinter import ttk

def generate_bingo_board():
    words = [
        "Freindly Player", "Aliance Betrail", "Get Krakened", 
        "Turn in a Chest of Sorrow", "Turn in a Chest of Rage",
        "Kill an Ancint Skelletion", "Finish A Legend of the Vail",
        "PVP Curse", "Sunken Sorrow Curse", "Another Crew in the Devals Roar",
        "Find a Breath of the Sea", "Baretrap a Player",
        "Tucker", "Turn in Ashen Tresure (Any)", "Gold Curse", "Tall Tail Crew",
        "Burning Blade", "Skelletion Ship", "Discover a Mermaid Gem",
        "Steal a Chest of Legends", "Firebomb an Enemy", "Give Gift", "Receve Gift", 
        "Be in the Storm", "Full Gallion", "Running Reaper", 
        "Solo Sloop", "Find A Kings Chest", "Find a Horn of Fair Wind", 
        "Siran Attack", "Catch A Trophy Fish", "Ashen Curse", "Keg an Enemy Ship",
        "Kill A Meglodon", "Grapple an Enemy or Thier Loot", "Disguised Player",
        "Active Fort of the Damned",
        
    ]
    
    random.shuffle(words)

    bingo_board = {
        'B': words[:5],
        'I': words[5:10],
        'N': words[10:15],
        'G': words[15:20],
        'O': words[20:25],
    }

    return bingo_board

def toggle_slot(button):
    """Toggle the bingo slot between marked (green) and unmarked (default)."""
    current_color = button.cget("bg")  # Correct attribute is "bg"
    if current_color == "red":
        button.config(bg="SystemButtonFace")  # Reset to default
    else:
        button.config(bg="red")  # Mark as completed

def display_bingo(board):
    root = tk.Tk()
    root.title("Bingo Board")

    columns = ['B', 'I', 'N', 'G', 'O']

    for col_index, col in enumerate(columns):
        label = ttk.Label(root, text=col, font=("Arial", 14, "bold"))
        label.grid(row=0, column=col_index, padx=10, pady=5)

        for row_index, value in enumerate(board[col]):
            btn = tk.Button(
                root, text=value, font=("Arial", 12),
                width=30, height=5, relief="raised", wraplength=100,
                bg="SystemButtonFace"  # Default color
            )
            # Now, correctly bind the button in the command
            btn.config(command=lambda b=btn: toggle_slot(b))
            
            btn.grid(row=row_index + 1, column=col_index, padx=5, pady=5)

    root.mainloop()

if __name__ == "__main__":
    bingo_board = generate_bingo_board()
    display_bingo(bingo_board)
