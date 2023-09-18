# Hands-on session Day 4: Incidence estimation

### 5 Initialization

As input the pipeline requires names of the covSonar file, the reference genome **(??)**, and binning parameters.
These variables are stored in [`config.yaml`](./config.yaml) and used as wildcards to create and link files with each other or as parameters for the binning. For more information about the YAML markup format refer to documentation: https://yaml.org


**Note:** paths to files in [`config.yaml`](./config.yaml) should be either:
- absolute,
- or relative to the main pipeline Snakefile,
- or relative to the working directory.

#### 5.1 Sample sequences - Change to covSonar!
The pipeline requires a file containing sequences, with the date in the sequence-name in GISAID format (date in format "%Y-%m-%d" at the end of header after a vertical bar).

For sequence files containing the date within the sequence-name, copy the file path and paste it into the variable **samples** of [`config.yaml`](./config.yaml):

  ```
  samples: "path/to/sequences/data"
  ```
If the headers in the sequence file do not contain the date, you can add it to headers using a custom script, given a meta table is provided along with the FASTA file.

In the field **group**, you can provide a name for the given samples, for example the country, location or any specifier for the given sequences, which is used for the plots.

  ```
  group: country
  ```


#### 5.2 Reported cases data file

To compare estimated population dynamics with reported active cases, provide the following parameters in the corresponding config field like this:

  ```
  reported_cases: ["path/to/reported_cases.csv", ",", date, new_cases, '%Y-%m-%d']
  ```
Alternatively, all arrays can be given in the configuration file as a list, like this:

  ```
  reported_cases:
    - path/to/reported_cases.csv
    - ","
    - date
    - new_cases
    - '%Y-%m-%d'    
  ```


where the first element of the list is the file name with format extension, the second element is the delimiter type in this file, date column name, active cases column name, and a format the date is stored in.

If no reported cases data is provided, leave the fields empty like this:

  ```
  reported_cases: []
  ```

#### 5.3 Reference sequence
Add the file path of reference/consensus sequence into the variable **consensus** of [`config.yaml`](./config.yaml).

  ```
  consensus: "path/to/consensus/sequence.fasta"
  ```

#### 5.4 Binning parameters
You also have to set the parameters for some of the binning methods in [`config.yaml`](./config.yaml).
You can set the number of sequences per bin, and the number of days.
Parameters can be given as an array or a list (see section above). Additionally, minimal bin size and maximal days span should be
provided.

  ```
  seq_per_bin: [20, 30]
  days_per_bin: [7, 10, 30]
  min_bin_size: 15
  max_days_span: 21
  min_days_span: 2
  ```

If parameter **seq_per_bin** is an empty list, a default mode with predefined fractions of sequences (2%, 5%, 7%) is used.

#### 5.5 Threshold for mutations

Low-abundance point mutations are filtered out, to avoid the consideration of sequence errors.
The cutoff for the amount of mutations at a certain sequence position in the whole dataset is set with:

  ```
  freq_cutoff: 2
  ```

#### 5.6 Trajectory smoothing parameters

  ```
  smoothing_bandwidth_phi: 7
  smoothing_bandwidth_mi: 7 
  ```


### 6 Run pipeline with demo dataset and configuration file
A demo sequence set and a reference sequence are included in repository folders [`demo`](./demo).
The directory contains a simulated data set with

- the reference sequence (????)
- a fasta file containing the newly emerging sequences over time (demo_samples.tsv)
- the underlying true number of emerging sequences (demo_reported_cases.tsv)
- the config file to call the pipeline with (demo_config.yaml)


To run the demo pipeline go into the repository where the GInPipe file is located and run:

```
snakemake --snakefile GInPipe --configfile demo/demo_config.yaml -j -d demo
```
The results will be stored in directory ***demo***.