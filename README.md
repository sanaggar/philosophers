# Philosophers

<p align="center">
  <img src="https://img.shields.io/badge/Language-C-blue?style=for-the-badge&logo=c" alt="C"/>
  <img src="https://img.shields.io/badge/Norm-42-00babc?style=for-the-badge" alt="42"/>
  <img src="https://img.shields.io/badge/Multithreading-POSIX-green?style=for-the-badge" alt="POSIX"/>
</p>

<p align="center">
  <strong>Implementation of the classic Dining Philosophers Problem</strong><br>
  A multithreading synchronization challenge using POSIX threads and mutexes
</p>

---

## About The Project

This project is an implementation of the **Dining Philosophers Problem**, a classic synchronization problem in computer science. It simulates philosophers sitting around a table, alternating between eating and thinking, while sharing forks with their neighbors.

The challenge lies in preventing **deadlock** and **race conditions** while ensuring no philosopher starves.

### Key Concepts Demonstrated

- **Concurrent Programming** — Thread creation, management and synchronization
- **Mutex Synchronization** — Protecting shared resources from race conditions
- **Deadlock Prevention** — Implementing strategies to avoid circular wait
- **Resource Management** — Proper allocation and cleanup of system resources
- **Precision Timing** — Millisecond-accurate scheduling and monitoring

---

## Technical Implementation

### Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      Main Thread                            │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐      ┌─────────┐    │
│  │ Philo 1 │  │ Philo 2 │  │ Philo 3 │ ...  │ Philo N │    │
│  └────┬────┘  └────┬────┘  └────┬────┘      └────┬────┘    │
│       │            │            │                │          │
│       └────────────┴────────────┴────────────────┘          │
│                           │                                  │
│                    ┌──────┴──────┐                          │
│                    │  Monitor    │                          │
│                    │   Thread    │                          │
│                    └─────────────┘                          │
└─────────────────────────────────────────────────────────────┘
```

### Synchronization Strategy

The program uses an **alternating fork acquisition pattern** to prevent deadlock:

- **Odd philosophers**: Take right fork first, then left fork
- **Even philosophers**: Take left fork first, then right fork

This breaks the circular wait condition that would otherwise cause deadlock.

### Thread Safety

| Mutex | Purpose |
|-------|---------|
| `fork_mutex[]` | One per fork, prevents simultaneous access |
| `meal_mutex` | Protects individual philosopher's meal data |
| `dead_mutex` | Guards the death flag for clean termination |
| `print_mutex` | Ensures atomic console output |

---

## Getting Started

### Prerequisites

- GCC compiler
- POSIX-compliant system (Linux/macOS)
- Make

### Installation

```bash
git clone https://github.com/sanaggar/philosophers.git
cd philosophers
make
```

### Usage

```bash
./philo <nb_philosophers> <time_to_die> <time_to_eat> <time_to_sleep> [nb_meals]
```

| Argument | Description |
|----------|-------------|
| `nb_philosophers` | Number of philosophers (and forks) |
| `time_to_die` | Time in ms before a philosopher dies without eating |
| `time_to_eat` | Time in ms it takes to eat |
| `time_to_sleep` | Time in ms spent sleeping |
| `nb_meals` | *(Optional)* Stop after each philosopher eats this many times |

### Examples

```bash
# 5 philosophers, standard timing
./philo 5 800 200 200

# With meal limit (stops after 7 meals each)
./philo 5 800 200 200 7

# Edge case: single philosopher (will die)
./philo 1 800 200 200

# Stress test: tight timing
./philo 4 410 200 200
```

### Output

```
0 1 has taken a fork
0 1 has taken a fork
0 1 is eating
200 1 is sleeping
200 2 has taken a fork
...
```

---

## Project Structure

```
philosophers/
├── philo.h              # Data structures and function prototypes
├── main.c               # Entry point and argument validation
├── parser.c             # Command-line argument parsing
├── init.c               # Initialization of structures and mutexes
├── create_and_join.c    # Thread creation and joining
├── routine_loop.c       # Philosopher thread routine
├── ft_eat.c             # Eating logic with fork management
├── sleep_and_think.c    # Sleep and think actions
├── checks.c             # Death and completion monitoring
├── time.c               # Precision timing utilities
├── utils.c              # Helper functions
├── destroy.c            # Cleanup and resource freeing
└── Makefile             # Build configuration
```

---

## Skills Demonstrated

<table>
<tr>
<td width="50%">

**Systems Programming**
- POSIX Threads (pthreads)
- Mutex synchronization
- Memory management
- System calls

</td>
<td width="50%">

**Software Engineering**
- Clean code architecture
- Error handling
- Edge case management
- Modular design

</td>
</tr>
</table>

---

## Build

```bash
make          # Compile
make clean    # Remove object files
make fclean   # Remove all generated files
make re       # Rebuild
```

**Compiler flags**: `-Wall -Wextra -Werror`

---

## Author

**sanaggar** — 42 Nice

---

<p align="center">
  <sub>Made with C and coffee at 42</sub>
</p>
