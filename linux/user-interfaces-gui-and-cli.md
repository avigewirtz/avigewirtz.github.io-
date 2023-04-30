# Command Line User Interface

A user interface defines the mechanism through which a user issues commands to a computer. Throughout computer history, there have been various types of user interfaces. The primary types of user interfaces are _graphical user interfaces (GUIs)_ and _command-line interfaces (CLIs)_.

### Graphical User Interface

The GUI is the default interface on macOS and Windows. In a GUI, users issue commands by clicking on graphical elements such as windows, icons, and menus. Common GUI elements include:

* **Windows**: Rectangular areas that display content or applications
* **Icons**: Small images representing files, folders, or applications
* **Menus**: Lists of options or commands that can be selected by the user
* **Buttons**: Graphical elements that perform specific actions when clicked

The GUI provides a visually intuitive and user-friendly interface, making it especially beneficial for less technical computer users.

### Command Line Interface

The CLI is a method of interacting with your computer where you issue commands via text rather than clicking or dragging graphical elements like buttons, icons, or menus. Examples of CLI usage include:

1. Opening an application: If a user wants to open an application such as Microsoft Word, they must issue a textual command like `open -a "Microsoft Word"` rather than double-clicking the Microsoft Word icon.
2. Moving a file: If a user wants to move a file from one folder to another, they must issue a textual command like `mv source_file destination_directory` rather than using the drag-and-drop paradigm.&#x20;

Both GUIs and CLIs have their advantages and limitations. GUIs are more intuitive and user-friendly, making them suitable for less technical users or for tasks that involve a lot of visual elements. On the other hand, CLIs offer more flexibility and control, making them the preferred choice for advanced users or for tasks that involve automation or repetitive actions. The choice between them depends on the user's level of expertise, personal preferences, and the specific task at hand.

## Terminal

The CLI is accessed via a _terminal_. In the nascent days of interactive computing, terminals were hardware devices, consisting of a keyboard for entering commands and a display unit for printing output. The first terminals were teletype machines, such as the Model 33 ASR shown in Figure 1, whose display unit was a paper-roll printer.

<figure><img src="https://lh4.googleusercontent.com/Sui_O3OmVfRuG7TS5Ro-pkF7IOJAAbL3Wxb5wHU2xvDIbpFmwGSHkM35HSD2Eic31K5unT9XBYsh63ta-eK33dyWUfQrfJKI48zSJjDUxw2m3LaRKU73PD2WRTUNqETK1FU1RoFPWQSqlph9K8Zoqc4" alt=""><figcaption><p>Figure 1: Teletype Model 33 ASR</p></figcaption></figure>



Teletypes fell out of use in the 1970s with the widespread adoption of video display terminals, such as the DEC VT100 shown in Figure 2. These terminals, unlike teletypes, employed screens for output display instead of paper-roll printers, making the CLI more efficient and user-friendly.

<figure><img src="https://lh6.googleusercontent.com/NkdzAjWbkb2-A2kfY9i6svIfMSKFxd_e_dUPZ-mfgbZlFPzQb4fPoe7ajYmIH002oDMQNhhzaZNy5oxAvvMX1JwGJo1gPfBO8DQSBbufeUWfDA_-C2qU51MmY5MzYIWTrWOErGR9kKb3RRmLos35cEo" alt=""><figcaption><p>Figure 2: DEC VT100 Terminal</p></figcaption></figure>



Today, hardware terminals have become obsolete. We now access the CLI via a software program called a _terminal emulator._ Terminal emulators are integrated into GUIs, but replicate the functionality of their hardware predecessors, allowing users to interact with their computer using text-based commands. An example of a terminal emulator is macOS's Terminal shown in Figure 3.&#x20;

<figure><img src="https://lh3.googleusercontent.com/D7N-haL7qpFme6x3NkICuiPbAG9LJd1JTni2tkEK-4htGMbvYfCnNBcFZUiOz4x5H8Z8A60wa8qMFF7_S6pO6ZwG9JD8vVTsygHgFSlIzpbZfO9fbw2tXSkdvkHnKvvgixPUvSYxHvA1wo6pd4NWH_0" alt=""><figcaption><p>Figure 3: macOS Terminal Application</p></figcaption></figure>

