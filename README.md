# CHESS_AI

A lightweight Python console chess game featuring a custom AI engine.

- AI is implemented with minimax search + alpha-beta pruning (`engine.py`).
- Human player inputs moves using UCI notation (`e2e4`, `b8c6`, etc.).
- Visual board output in ASCII format using `python-chess`.

---

## 📁 Repository Structure

- `main.py`: CLI game loop, input/output, and turn management.
- `engine.py`: evaluation function and AI move search (`miniMax`, `getAiMove`).
- `README.md`: project documentation.
- `requirements.txt`: Python dependencies.

---

## 🛠️ Requirements

- Python 3.8 or newer
- `python-chess`

Install dependency:

```bash
pip install -r requirements.txt
```

If using `venv`:

```bash
python -m venv venv
venv\Scripts\activate      # Windows
pip install -r requirements.txt
```

---

## ▶️ Running the Game

In project folder:

```bash
python main.py
```

Expected start-up output:

```
--- Welcome to My Chess AI (VIT BYOP Project) ---
Type your move in UCI format (e.g., e2e4)
```

---

## ♟️ Gameplay Details

- AI plays White, user plays Black.
- AI move displayed as `AI Move: e2e4`.
- User move prompt:

  - Enter UCI
  - Type `exit` to quit on your turn.

- Illegal move validation:

  - If input cannot be parsed, it prints "Invalid input..."
  - If move is not legal, it prints "That move isn't legal..."

- Game end is detected by `python-chess`:

  - Checkmate
  - Stalemate
  - Insufficient material / draw conditions

- Final result prints as `Final Result: 1-0`, `0-1`, or `1/2-1/2`.

---

## 🤖 AI Engine

Main functions in `engine.py`:

- `calculateScore(board)`
  - Material-based scoring with weights:
    - Pawn 100, Knight 320, Bishop 330, Rook 500, Queen 900, King 20000
  - Checkmate returns large positive/negative result.

- `miniMax(board, depth, alpha, beta, isMaximizing)`
  - Recursively searches legal moves.
  - Alpha-beta pruning to reduce branches.

- `getAiMove(board, currentDepth)`
  - Scans legal moves, picks maximum evaluation.

### Depth tuning

Default in `main.py`:

```python
aiMove = engine.getAiMove(currentBoard, 3)
```

- `3`: fast, moderate skill
- `4`: stronger but slower
- `5+`: exponential time growth

---

## 🧪 Example session

1. Start program
2. AI plays `e2e4`
3. User enters `e7e5`
4. AI calculates and plays next move
5. Continue until game over

---

## 🛠️ Customization Ideas

- Support human White and AI Black (swap turns in `main.py`).
- Add opening book for early moves.
- Add piece-square tables or positional heuristics in `calculateScore`.
- Enable engine tournaments and benchmarking with time limits.
- Add GUI (e.g., `pygame`, web interface) while keeping current engine.

---

## 🐞 Troubleshooting

- "ModuleNotFoundError: No module named 'chess'" -> run `pip install -r requirements.txt`.
- Python 2 is unsupported. Use Python 3.
- Unexpected behavior on long searches: reduce depth.
