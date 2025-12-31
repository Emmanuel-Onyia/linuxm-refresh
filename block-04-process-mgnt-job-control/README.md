# Block 04 — Process Management & Job Control

This block focuses on **runtime process control in Linux**. While previous blocks dealt with file permissions and access control, Block 04 shifts attention to **actively running programs**—how they are created, managed, paused, resumed, prioritized, and terminated.

These concepts are foundational for **system administration, cloud support, and incident troubleshooting**.

---

## Objectives

By completing this block, the following competencies were developed:

- Understanding what a **process** is at the kernel level
- Distinguishing between **processes** and **jobs**
- Inspecting running processes and parent-child relationships
- Managing foreground and background execution
- Sending and handling process signals safely
- Understanding and manipulating process priority using `nice` and `renice`

---

## Key Concepts Covered

- Process lifecycle (creation → execution → termination)
- PID vs PPID
- Jobs vs processes
- Foreground vs background execution
- Linux signals
- Safe vs forceful process termination
- Process priority and CPU scheduling
- Nice values and fairness

---

## Drill 01 — Process Inspection (`ps`)

### Focus
Understanding how to view and interpret running processes.

### Commands Used
```bash
ps
ps -f
ps aux
```

### Key Takeaways

- ps shows only processes associated with the current terminal
- ps aux displays all system processes
- PPID represents the parent process, not priority
- Knowing process ownership is essential for permissions, security, and troubleshooting


## Drill 02 — Foreground vs Background Jobs

### Focus
Understanding shell-level job control.

### Commands Used
```bash
sleep 60
sleep 60 &
jobs
bg
fg
```

### Key Takeaways

- Jobs are managed by the shell
- Processes are managed by the kernel
- Job IDs (%1) are not the same as PIDs
- Background jobs still terminate when the terminal closes
- Only stopped (not terminated) jobs can be resumed


## Drill 03 — Signals and Process Termination

### Focus
Safely stopping, pausing, resuming, and terminating processes.

### Commands Used
```bash
kill <PID>
kill -9 <PID>
kill -STOP <PID>
kill -CONT <PID>
killall <process_name>
```

### Key Takeaways

- SIGTERM (15) should always be attempted first
- SIGKILL (9) is a last resort and bypasses cleanup
- Stopped processes can be resumed
- Terminated processes must be restarted
- Signals are the primary mechanism for process control in Linux


## Drill 04 — Process Priority and nice

### Focus
Understanding CPU scheduling and fairness.

### Commands Used
```bash
nice -n 10 sleep 120 &
renice 15 -p <PID>
ps -o pid,ni,cmd -p <PID>
```

### Key Takeaways

- Nice values range from -20 (highest priority) to 19 (lowest priority)
- Higher nice value = lower CPU priority
- Regular users can only lower priority
- Priority affects CPU time, not killability
