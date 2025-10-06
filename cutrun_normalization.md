# Normalization Methods for CUT&RUN, CUT&Tag, and CUTAC

## Spike-in Scaling

Exogenous DNA (i.e. E. coli or Drosophila) is added to the stop buffer of the CUT&RUN or CUT&Tag reaction. Spike-in reads are mapped separately, for example, to the E.coli genome, in addition to reads mapped to the target/primary genome (i.e. human, mouse, etc.). The assumption is that the ratio of reads mapped to the target genome compared to the spike-in genome is the same across all samples that were processed in the same batch and using the same number of cells. 

Using a constant C, we define the **scaling factor** as:
$$\text{S} = \frac{\text{C}}{\text{Fragments mapped to E. coli genome}}$$

Then, we apply the scaling factor to normalize the target reads:
$$\text{Normalized coverage} = (\text{Target genome coverage}) \times S$$

**Advantages:**
- Accounts for technical variability between samples
- Corrects for differences in cell number and antibody efficiency
- Particularly useful when comparing samples with different signal strengths

**Disadvantages:**
- Requires careful spike-in addition at the experimental stage
- Assumes uniform spike-in distribution
- May not work well if spike-in percentage varies significantly

## Library Size Normalization (Total Count)

This method normalizes by the total number of mapped reads in each sample, assuming that the total amount of sequencing obtained is proportional to the amount of material in each sample.

**Scaling factor:**
$$\text{S} = \frac{\text{C}}{\text{Total mapped reads}}$$

**Normalized coverage:**
$$\text{Normalized coverage} = (\text{Raw coverage}) \times S$$

where C is typically set to the minimum library size across all samples, or to a standard value like 1 million or 10 million.

**Advantages:**
- Simple and straightforward
- No additional experimental steps required
- Works when spike-ins are not available

**Disadvantages:**
- Assumes similar signal-to-noise ratios across samples
- Can be biased if global changes in binding occur
- Not ideal when samples have very different enrichment levels

## CPM/RPM Normalization

**Counts Per Million (CPM)** or **Reads Per Million (RPM)** normalizes coverage values to a standard library size of 1 million reads.

$$\text{CPM} = \frac{\text{Raw counts}}{\text{Total mapped reads}} \times 10^6$$

For bigWig files or coverage tracks:
$$\text{RPM coverage} = \frac{\text{Raw coverage}}{\text{Total mapped reads}} \times 10^6$$

**Advantages:**
- Makes samples directly comparable
- Intuitive interpretation (counts per million reads)
- Standard method in many analysis pipelines

**Disadvantages:**
- Same limitations as library size normalization
- Doesn't account for fragment length differences

## RPGC Normalization (Reads Per Genomic Content)

Also known as **1x depth normalization**, this method normalizes by both library size and effective genome size.

$$\text{RPGC} = \frac{\text{Number of reads}}{\text{Scaling factor}}$$

where:
$$\text{Scaling factor} = \frac{\text{Total mapped reads} \times \text{Fragment length}}{\text{Effective genome size}}$$

The effective genome size is the portion of the genome that is mappable with the given read length.

**Advantages:**
- Accounts for effective genome size
- Useful for comparing across different genomes
- Implemented in deepTools

**Disadvantages:**
- Requires knowing the effective genome size
- Still assumes similar global enrichment

## IgG Control Subtraction

Background signal is estimated using an IgG control experiment and subtracted from the target signal.

$$\text{Normalized signal} = \text{Target signal} - (\text{IgG signal} \times \text{scaling factor})$$

The scaling factor can be determined by:
- Library size ratio between target and IgG
- Spike-in normalization factors
- Or set to 1 if both are already normalized

**Advantages:**
- Removes non-specific binding signal
- Improves signal-to-noise ratio
- Identifies true binding sites

**Disadvantages:**
- Requires additional IgG control experiment
- May overcorrect in low-signal regions
- Negative values require handling (typically set to 0)

## Quantile Normalization

This method makes the distribution of signal values identical across all samples by ranking values and averaging across samples.

**Steps:**
1. Rank all values in each sample
2. For each rank, compute the mean value across all samples
3. Replace each value with the mean of its rank position

**Advantages:**
- Removes systematic biases
- Makes distributions comparable
- Useful for batch effect removal

**Disadvantages:**
- Assumes samples should have similar distributions
- Can obscure true biological differences
- Not recommended if samples are expected to be very different

## Recommendations

**For standard experiments:**
- Use spike-in normalization when available (gold standard)
- Fall back to CPM/RPM if spike-ins were not used
- Always include IgG controls for background subtraction

**For differential binding analysis:**
- Consider using tools with built-in normalization (DiffBind, csaw)
- These often use TMM or DESeq2-style normalization

**For visualization:**
- CPM/RPM is often sufficient for browser tracks
- Spike-in normalization provides the most accurate comparison
- Consider log-transformation for better visualization of fold changes

## Common Pitfalls

- **Not normalizing:** Can lead to false positives due to library size differences
- **Over-normalization:** Applying multiple normalizations can introduce artifacts
- **Mixing methods:** Be consistent across all samples in an experiment
- **Ignoring spike-in quality:** Low spike-in reads (<1%) may not be reliable for normalization
