# 🧩 Socket Communication Programs

This project consists of **two intercommunicating C++ programs** that demonstrate:
- multi-threaded data handling with a shared buffer,
- synchronization between threads without global flags,
- client-server communication over sockets.

---

## 🧠 Program Overview

### 🔧 Program 1: Data Preprocessing & Client
- Accepts numeric input (up to 64 digits) from the user.
- Validates input (digits only), sorts it in descending order.
- Replaces even digits with the letters **"KV"**.
- Adds processed strings to a shared buffer between two threads.
- Second thread reads the buffer, extracts numeric values, calculates their sum, and sends it to Program 2 via sockets.

> ⚠ Thread interaction is **synchronized using condition variables** — no busy-waiting or global flags.

> ⚠ Robust socket logic ensures user input continues uninterrupted even if Program 2 crashes or reconnects.

---

### 🌐 Program 2: Socket Server & Validator
- Listens for incoming socket messages from Program 1.
- For each received message (sum of digits):
  - If **length > 2** and **value % 32 == 0**, displays valid message.
  - Else, reports an error.
- Waits for reconnection if Program 1 restarts.

---

## 🚀 Build Instructions (Linux, GCC, CMake ≥ 3.30.2)

### 🔨 Build & Run Program 1 (Client)
```bash
cd build_program_1  # Create a separate build folder
cmake ../program_1  # Provide relative path to Program 1 sources
make
./program_1        # Run Program 1
```

### 🌐 Build & Run Program 2 (Server)
```bash
cd build_program_2
cmake ../program_2
make
./program_2
```

---

## 📁 Project Structure
```
infotecs-socket-task/
├── program_1/
│   ├── CMakeLists.txt
│   ├── main.cpp
│   └── ...
├── program_2/
│   ├── CMakeLists.txt
│   ├── main.cpp
│   └── ...
```

> ⚠ Do **not** include intermediate build files or binaries in the archive.

---

## ✅ Requirements Met
- Two-thread system with buffer, condition variable sync
- Input processing with transformation logic
- Safe and reconnectable socket communication
- Validations and protocol logic in server
- Modular, clean C++ code with structured interface design





