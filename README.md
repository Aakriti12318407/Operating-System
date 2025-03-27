def check_node_health(self):
    """
    Check each node directory and report whether it exists (healthy) or is missing (failed).
    Returns a dict: {node_directory: True (healthy) or False (failed)}
    """
    status = {}
    for node in self.node_directories:
        status[node] = os.path.exists(node)
    return status

def display_node_health(self):
    status = self.check_node_health()
    for node, healthy in status.items():
        if healthy:
            print(f"Node '{node}': Healthy")
        else:
            print(f"Node '{node}': FAILED")

def recover_node(self, node_directory):
    """
    Attempt to recover a failed node by copying files from a healthy node.
    Uses the node at recovery_source_index as the source.
    """
    if os.path.exists(node_directory):
        print(f"Node '{node_directory}' is already healthy.")
        return
    source_node = self.node_directories[self.recovery_source_index]
    if not os.path.exists(source_node):
        print(f"Source node '{source_node}' is not available for recovery.")
        return
    os.makedirs(node_directory)
    for item in os.listdir(source_node):
        src = os.path.join(source_node, item)
        dst = os.path.join(node_directory, item)
        if os.path.isfile(src):
            shutil.copy(src, dst)
    print(f"Recovered node '{node_directory}' using data from '{source_node}'.")

def auto_recover(self):
    """
    Automatically recover any failed nodes by checking their health and triggering recovery.
    """
    status = self.check_node_health()
    for node, healthy in status.items():
        if not healthy:
            self.recover_node(node)

def start_monitoring(self):
    """
    Start the monitoring loop that displays node health and automatically recovers failed nodes.
    """
    self._monitoring = True
    print("Monitoring started. Press Ctrl+C to stop or use the interactive menu to stop.")
    try:
        while self._monitoring:
            self.display_node_health()
            self.auto_recover()
            time.sleep(self.monitor_interval)
    except KeyboardInterrupt:
        print("Monitoring interrupted.")

def stop_monitoring(self):
    self._monitoring = False
    print("Monitoring stopped.")

