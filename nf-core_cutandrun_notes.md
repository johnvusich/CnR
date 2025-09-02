# nf-core/cutandrun notes

## Cleaning Peak Files

The pipeline will output SEACR peak files for each sample. Using the SEACR 'relaxed' setting, the pipeline will output sample peaks with the naming format as sample_name.seacr.peaks.relaxed.bed

To clean the peaks to be used in deepTools matrix and heatmaps, the pipeline uses awk to remove everything except the chromosome number and coordinates. To do it yourself on the commandline, here is an example script:

```bash
awk  '{split($6, summit, ":"); split(summit[2], region, "-"); print summit[1]"\t"region[1]"\t"region[2]}' sample_name.seacr.peaks.relaxed.bed  > sample_name.max_signal.awk.txt
```

Loop over all of the `.seacr.peaks.relaxed.bed` files in your directory using the `awk` command on each one and writing the output file using the same prefix by running this script:

```bash
for f in *.seacr.peaks.relaxed.bed
do
    base="${f%.seacr.peaks.relaxed.bed}"
    awk '{split($6, summit, ":"); split(summit[2], region, "-"); print summit[1]"\t"region[1]"\t"region[2]}' "$f" > "${base}.max_signal.awk.txt"
done
```
