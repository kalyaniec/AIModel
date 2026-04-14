import psutil
from datetime import datetime

def get_system_usage():
    print("=" * 50)
    print(f"System Usage Snapshot - {datetime.now()}")
    print("=" * 50)

    # CPU usage
    cpu_percent = psutil.cpu_percent(interval=1)
    print(f"\nTotal CPU Usage: {cpu_percent}%")

    # Memory usage
    memory = psutil.virtual_memory()
    print(f"Total Memory: {memory.total / (1024**3):.2f} GB")
    print(f"Used Memory : {memory.used / (1024**3):.2f} GB")
    print(f"Memory Usage: {memory.percent}%")

def get_processes():
    print("\n" + "=" * 50)
    print("Running Processes:")
    print("=" * 50)

    processes = []

    for proc in psutil.process_iter(['pid', 'name', 'cpu_percent', 'memory_percent']):
        try:
            processes.append(proc.info)
        except (psutil.NoSuchProcess, psutil.AccessDenied):
            continue

    # Sort by CPU usage (descending)
    processes = sorted(processes, key=lambda p: p['cpu_percent'], reverse=True)

    # Print top processes
    print(f"{'PID':<10}{'Name':<25}{'CPU %':<10}{'Memory %':<10}")
    print("-" * 55)

    for p in processes[:15]:  # show top 15
        print(f"{p['pid']:<10}{p['name'][:24]:<25}{p['cpu_percent']:<10}{p['memory_percent']:.2f}")

if __name__ == "__main__":
    get_system_usage()
    get_processes()