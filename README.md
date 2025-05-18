import pandas as pd
import time
import os

log_path = r"C:\Snort\log\alert.csv"  # Raw string for Windows paths

def read_alerts():
    print("Monitoring Snort logs...")
    while True:
        try:
            if os.path.exists(log_path):
                df = pd.read_csv(log_path)
                if not df.empty:
                    print("\n=== New Alerts ===")
                    print(df[['timestamp', 'msg', 'src_ip', 'dst_ip']])
                    # Clear the log file after reading (optional)
                    open(log_path, 'w').close()
            else:
                print("Log file not found. Check Snort configuration!")
        except Exception as e:
            print(f"Error: {e}")
        time.sleep(5)  # Check every 5 seconds

if __name__ == "__main__":
    read_alerts()
