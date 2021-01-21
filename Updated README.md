# ACM Research Coding Challenge (Spring 2021)

# Genome analysis

Genomic analysis is the identification, measurement or comparison of genomic features such as DNA sequence, structural variation, gene expression, or regulatory and functional element annotation at a genomic scale.



## My Solution

I'm using a top down approach. After loading it in the sequence, I created an empty diagram, then added an (empty) track, and to that added an (empty) feature set.
I take each gene SeqFeature object in our SeqRecord, and use it to generate a feature on the diagram and color them blue, alternating between a dark blue and a light blue.
Now drawing a circular genome map and output it as a PNG file. This happens in two steps, first we call the draw method, which creates all the shapes using ReportLab objects. Then we call the write method which renders these to the requested file format


## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install biopython and reportlab.

```bash

pip install biopython
pip install reportlab

```

## Usage 

```python

# Visualization and graphs
from reportlab.lib import colors
from reportlab.lib.units import cm
from Bio.Graphics import GenomeDiagram
from Bio import SeqIO
# reading the file again for graph
record = SeqIO.read("Genome.gb", "genbank")


gd_diagram = GenomeDiagram.Diagram("Genome analysis")
gd_track_for_features = gd_diagram.new_track(1, name="Annotated Features")
gd_feature_set = gd_track_for_features.new_set()

for feature in record.features:
    if feature.type != "gene":
        #Exclude this feature
        continue
    if len(gd_feature_set) % 2 == 0:
        color = colors.blue
    else:
        color = colors.lightblue
    gd_feature_set.add_feature(feature, color=color, label=True)



gd_diagram.draw(format="circular", circular=True, pagesize=(20*cm,20*cm),
                start=0, end=len(record), circle_core=0.7)
gd_diagram.write("genome circular.png", "PNG")
```
## Results
Circular Genome Map
![genome circular]       -  https://github.com/MahnoorFatima12/ACM-Research-Coding-Challenge-S21/blob/main/genome%20circular.png

![genome circular bonus] - https://github.com/MahnoorFatima12/ACM-Research-Coding-Challenge-S21/blob/main/genome%20circular%20Bonus.png
