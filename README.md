def check_node_health(self):
    """
    Check each node directory and report whether it exists (healthy) or is missing (failed).
    Returns a dict: {node_directory: True (healthy) or False (failed)}
    """
    status = {}
    for node in self.node_directories:
        status[node] = os.path.exists(node)
    return status
