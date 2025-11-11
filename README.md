<h1>ExpNo 9: Solve Wumpus World Problem using Python demonstrating Inferences from Propositional Logic</h1> 

```
Name         : KAMALESH S
Register No. : 212223040083
```

<H3>Aim:</H3>
<p>
    To solve  Wumpus World Problem using Python demonstrating Inferences from Propositional Logic
</p>
<h1>Problem Description</h1>
<hr>
<h2>Wumpus World</h2>
<hr>
The Wumpus world is a simple world example to illustrate the worth of a knowledge-based agent and to represent knowledge representation.

The figure below shows a Wumpus world containing one pit and one Wumpus. There is an agent in room [1,1]. The goal of the agent is to exit the Wumpus world alive. The agent can exit the Wumpus world by reaching room [4,4]. The wumpus world contains exactly one Wumpus and one pit. There will be a breeze in the rooms adjacent to the pit, and there will be a stench in the rooms adjacent to Wumpus.

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/cd6b68dc-c79f-4dcb-8126-04da90d65912)

<center>Wumpus World Representation</center>
<p>
This is a python program that uses propositional logic sentences to check which rooms are safe. 

It is assumed that there will always be a safe path that the agent can take to exit the Wumpus world. The logical agent can take four actions: Up, Down, Left and Right. These actions help the agent move from one room to an adjacent room. The agent can perceive two things: Breeze and Stench.
</p>

## Code
```
wumpus = [
    ["Safe", "Breeze", "PIT", "Breeze"],
    ["Smell", "Safe", "Breeze", "Safe"],
    ["WUMPUS", "GOLD", "PIT", "Breeze"],
    ["Smell", "Safe", "Breeze", "PIT"]
]

row, column = 0, 0
arrow = True
player = True
score = 0

safe_cells = set()
unsafe_cells = set()
visited = set()

def neighbors(r, c):
    """Return all valid neighboring coordinates (up, down, left, right)."""
    possible = []
    if r > 0: possible.append((r - 1, c))
    if r < 3: possible.append((r + 1, c))
    if c > 0: possible.append((r, c - 1))
    if c < 3: possible.append((r, c + 1))
    return possible

def infer_logic(r, c):
    """Perform simple propositional logic inference based on percepts."""
    cell = wumpus[r][c]
    visited.add((r, c))

    if cell == "Safe":
        safe_cells.add((r, c))

    elif cell == "Breeze":
        for (x, y) in neighbors(r, c):
            if (x, y) not in visited:
                unsafe_cells.add((x, y))
        print(f"Inference: Breeze at {(r+1,c+1)} ⇒ One of {neighbors(r,c)} has a PIT.")

    elif cell == "Smell":
        for (x, y) in neighbors(r, c):
            if (x, y) not in visited:
                unsafe_cells.add((x, y))
        print(f"Inference: Smell at {(r+1,c+1)} ⇒ One of {neighbors(r,c)} has the WUMPUS.")

    elif cell == "PIT":
        unsafe_cells.add((r, c))
        print(f"Inference: Confirmed PIT at {(r+1,c+1)}")

    elif cell == "WUMPUS":
        unsafe_cells.add((r, c))
        print(f"Inference: Confirmed WUMPUS at {(r+1,c+1)}")

    elif cell == "GOLD":
        safe_cells.add((r, c))
        print(f"Inference: GOLD found at {(r+1,c+1)} ⇒ Cell safe & goal reached!")

    if cell not in ["Breeze", "Smell", "PIT", "WUMPUS"]:
        for (x, y) in neighbors(r, c):
            if (x, y) not in unsafe_cells:
                safe_cells.add((x, y))
        print(f"Inference: No danger sensed ⇒ All neighbors of {(r+1,c+1)} are SAFE.")

while player:
    print("\n===================================")
    print(f"Current position: ({row+1}, {column+1}) -> {wumpus[row][column]}")
    infer_logic(row, column)

    print(f"Known safe cells: {[(r+1,c+1) for (r,c) in safe_cells]}")
    print(f"Known unsafe cells: {[(r+1,c+1) for (r,c) in unsafe_cells]}")

    if wumpus[row][column] == "GOLD":
        score += 1000
        print("\n Congratulations! You found the GOLD!")
        print(f" Final Score: {score}")
        break

    if wumpus[row][column] == "WUMPUS":
        score -= 1000
        print("\n The Wumpus got you! You die.")
        print(f"💯 Final Score: {score}")
        break
    elif wumpus[row][column] == "PIT":
        score -= 1000
        print("\n You fell into a PIT!")
        print(f"💯 Final Score: {score}")
        break

    move = input("\nMove (u=up, d=down, l=left, r=right, q=quit): ").lower()

    if move == "u" and row > 0:
        row -= 1
    elif move == "d" and row < 3:
        row += 1
    elif move == "l" and column > 0:
        column -= 1
    elif move == "r" and column < 3:
        column += 1
    elif move == "q":
        print("Game exited.")
        break
    else:
        print("Invalid or blocked move! Try again.")

    score -= 1
print("\nGame Over.")

```

<hr>
<h1>Sample Input and Output:</h1>
<img width="1610" height="964" alt="code" src="https://github.com/user-attachments/assets/dbb463dc-c2b2-44c9-aaa9-265356e7f0b5" />
<img width="1196" height="276" alt="output" src="https://github.com/user-attachments/assets/fedde023-7b68-40c2-abf0-680fa0d2db1f" />

<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8696111a-a4a7-47cb-ba4b-43a4ef88573f)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/4be5bf06-79fa-4fa0-9334-38a33f06060b)

## Result:
The Wumpus World Problem is demonstrated and solved using Python.
