# PCA-vs.-PcoA-comparison-figure-by-python
#overlapped feature: matrix decomposition plus distinguished: co-variance vs. distance matrix (sklearn.decomposition()) → extracting eigenvector 
#distinguished feature：PCA hypothesis of linear data pattern; PCoA requires inter-sample Euclidean distance (in contrast to Geodesic Distance bio ISOMAP of manifold learning) with flexibility for data patterns 

from graphviz import Digraph

dot = Digraph("PCA_vs_PCoA_Workflow", format="png")

# Shared steps
dot.node("A", "Input data matrix\n(samples × features)")
dot.node("B", "Preprocessing\n(filtering, normalization)")
dot.node("C", "Distance / covariance representation")

# PCA-specific
dot.node("D1", "Covariance / correlation matrix")
dot.node("E1", "Eigen decomposition\n(linear)")
dot.node("F1", "Principal components")

# PCoA-specific
dot.node("D2", "Distance matrix\n(Bray–Curtis, UniFrac, etc.)")
dot.node("E2", "Double centering")
dot.node("F2", "Principal coordinates")

# Plotting
dot.node("G", "Ordination plot\n(PC1 vs PC2)")

# Edges
dot.edges([
    ("A", "B"),
    ("B", "C"),

    ("C", "D1"),
    ("D1", "E1"),
    ("E1", "F1"),
    ("F1", "G"),

    ("C", "D2"),
    ("D2", "E2"),
    ("E2", "F2"),
    ("F2", "G")
])

dot
