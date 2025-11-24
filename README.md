# **personalCLI**

A lightweight Windows-only command-line assistant built in Python.
It allows you to open apps, close programs, search the web, open YouTube in Brave, fetch battery level, and run custom shortcuts from a simple terminal-like interface.

---

## **Features**

* Launch Windows apps (`chrome`, `vscode`, `spotify`, etc.)
* Open websites and run instant web searches
* YouTube search in Brave browser
* Kill/close running applications
* Check battery status
* System commands (shutdown, restart)
* Easily expandable with new commands
* Simple REPL-style interface (`$ command`)

---

## **Supported Commands**

| Command           | Example                | Description                         |                             
| ----------------- | ---------------------- | ----------------------------------- | 
| `open <app        | url>`                  | `open chrome`                       | 
| `close <app>`     | `close chrome`         | Kills an application (`taskkill`)   |                             
| `youtube <query>` | `youtube lofi beats`   | Searches YouTube (opens in Brave)   |                             
| `google <query>`  | `google python typing` | Google search                       |                             
| `wiki <query>`    | `wiki tensor`          | Wikipedia search                    |                             
| `shutdown`        | `shutdown`             | Shutdown (with confirmation)        |                             
| `restart`         | `restart`              | Restart (with confirmation)         |                             
| `battery`         | `battery`              | Shows battery % and charging status |                             
| `help`            | `help`                 | Prints available commands           |                             
| `exit`            | `exit`                 | Quits the CLI                       |                             

Additional placeholder commands exist but are not implemented yet.

---

## **Installation**

### Requirements

* Windows
* Python 3.9+
* `psutil` installed:

```
pip install psutil
```

### Run

```
python main.py
```

You will see:

```
$ 
```

You may now enter commands.

---

## **How App Launching Works**

Applications are mapped manually here:

```python
__appMap__ = {
    "chrome": "chrome.exe",
    "vscode": "code.exe",
    "notepad": "notepad.exe",
    "spotify": "spotify.exe",
    "brave": "brave.exe"
}
```

The launcher:

1. Checks if the argument is a URL
2. Checks if it’s a valid path
3. Checks in `__appMap__`
4. Searches common install directories
5. Falls back to PATH lookup (`shutil.which`)

---

## **YouTube in Brave**

YouTube commands always use Brave:

```python
brave = r"C:\Program Files\BraveSoftware\Brave-Browser\Application\brave.exe"
```

To change browsers, simply edit this path.

---

## **Process Closing**

Closing an app uses:

```
taskkill /IM <app>.exe /F
```

A confirmation prompt prevents accidental termination.

---

## **Extending personalCLI**

To add new commands:

1. Add the command name into `__commands__`
2. Add handling logic inside `checkType()`
3. Add a function for the behavior (e.g., play music, control volume, etc.)

This design keeps the project modular and easy to grow.

---

## **Future Enhancements**

* Volume/music control
* Weather & news API
* Screenshot and screen recording
* File management (move, copy, etc.)
* System stats
* Plugin system
* Voice input


