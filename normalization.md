# Normalization Methods for CUT&RUN, CUT&Tag, and CUTAC

## Spike-in Scaling

Exogenous DNA (i.e. E. coli or Drosophila) is added to the stop buffer of the CUT&RUN or CUT&Tag reaction. Spike-in reads are mapped seperately, for example, to the E.coli genome, in addition to reads mapped to the target/primary genome (i.e. human, mouse, etc.) . The assumption is that the ratio of reads mapped to the target genome compared to the spike-in genome is the same across all samples that were processed in the same batch and using the same number of cells. 

Using a constant C, we define the **scaling factor** as:
$$\text{S} = \frac{\text{C}}{\text{Fragments mapped to E. coli genome}}$$

Then, we apply the scaling factor to normalize the target reads:
$Normalized coverage = (Target gonome coverage) * S$
