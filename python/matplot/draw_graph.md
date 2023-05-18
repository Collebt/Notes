```python
import matplotlib.pyplot as plt
import networkx as nx

# Create a graph object
G = nx.Graph()

# Add nodes to the graph with their positions and weights
nodes = [(0, 0, 5), (1, 1, 10), (2, 2, 15), (3, 3, 20)]
for node in nodes:
    G.add_node(node[0], pos=(node[1], node[2]), weight=node[2])

# Add edges to the graph with their weights
edges = [(0, 1, 3), (0, 2, 5), (1, 2, 2), (2, 3, 8)]
for edge in edges:
    G.add_edge(edge[0], edge[1], weight=edge[2])

# Draw the graph with node colors and edge widths
pos = nx.get_node_attributes(G, 'pos')
weights = nx.get_node_attributes(G, 'weight')
edge_widths = nx.get_edge_attributes(G, 'weight').values()

plt.figure(figsize=(8, 8))
nx.draw_networkx_nodes(G, pos, node_color=list(weights.values()), cmap=plt.cm.Reds)
nx.draw_networkx_edges(G, pos, width=list(edge_widths))
nx.draw_networkx_labels(G, pos, labels={n: str(n) for n in G.nodes()}, font_size=12, font_color='white', label_pos=0.5, ax=plt.gca())
plt.axis('off')
plt.show()

```

\



