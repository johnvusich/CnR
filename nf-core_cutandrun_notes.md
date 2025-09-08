# nf-core/cutandrun notes

## Generating Genome Track Images in IGV
In the MSU HPCC OnDemand website, click the "Interactive Apps" dropdown menu and select "Interactive Desktop". Input the amount of resources needed to run IGV and output image files (e.g. 4 hours, 8 cores, 16 GB of memory) and launch the desktop.

When you open the interactive desktop, it will open a new browser tab with TurboVNC remote desktop from your Home Directory. Click the upper left "Menu" dropdown, and select the "Mate Terminal" app. Enter the following lines of code to launch the IGV app:
```bash
module load IGV/2.16.0-Java-11
igv.sh
```
Note: you can launch IGV pre-loaded with the reference genome you used to align the sequencing reads. For example, for mm39 reference genome, run the following lines in the terminal:
```bash
module load IGV/2.16.0-Java-11
igv.sh -g mm39
```

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
