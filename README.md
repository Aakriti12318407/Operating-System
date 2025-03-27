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
