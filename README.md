# ProbAsn
Probabilistic assignment of organic crystals

This is the code for the paper [Bayesian Probabilistic Assignment of Chemical Shifts in Organic Solids](https://doi.org/10.1126/sciadv.abk2341).

# Installation

## Python

You first need to install the Python package using pip. This will install all the required dependencies.

> pip install .

Alternatively, a Python environment containing all the required libraries can be installed by running the "install_env.sh" script (requires [anaconda](https://www.anaconda.com) to be installed)

## Database

The database (updated with predictions from [ShiftML2](https://doi.org/10.1021/acs.jpcc.2c03854)) is available from this [Materialscloud archive](https://archive.materialscloud.org/deposit/records/1824), file [db.zip](https://archive.materialscloud.org/record/file?filename=db.zip&record_id=1824)

To download the database, you can enter Python in the `examples` directory, import the `ProbAsn` package and use the `download_database()` function:

> cd examples
>
> python
>
>> import ProbAsn
>>
>> ProbAsn.utils.download_database()
>>
>> quit()

Alternatively, download the file and place it in the `db` directory.

Then, you should be good to go!

# Running the software

To perform the assignment of a molecule, prepare an input file as described in `input_file_description.md` or modify an existing input file that you can find in the `example` directory. Then, perform the assignment by running:

> python run.py input_file.in

Alternatively, you can run the `run.ipynb` notebook and modify the input file in cell 2.

# Output files

The `output` directory will contain the output of the software. Several directories and files will be created. The exact name of the files will change depending on the analysis performed. The output files are described below, with parts of filenames subject to change indicated by square brackets:

- structure.[mol]: Molecular structure (useful to identify the atom labeling)
- graphs_[C]/: Directory containing plots of the graphs identified for the element of interest in the molecule.
- distribs_[C]/: Directory containing plots of the statistical distributions of chemical shifts for each nucleus considered in the molecule.
- distribs_[C].pdf: Plot of all distributions of chemical shifts, labelled. Labels are indicated on top of each distribution for 1D simulations, and above the plot and sorted from left to right by decreaasing chemical shift value in the x-axis for 2D simulations.
- distribs\_[C]\_with\_exp.pdf: Plot of all distributions of chemical shifts, labelled, with black bars (1D simulation) / dots (2D simulation) indicating experimental shifts.
- probs_[C]/: Directory containing the prior and marginal individual assignment probabilities, as well as global assignment probabilities.
  - prior_probs.dat: Table of prior individual assignment probabilities
  - prior_probs_0.pdf: Plot of prior individual assignment probabilities
  - assignment_probs.dat: Tables of global assignments generated along with their probabilities
  - marginal_probs.dat: Tables of marginal individual assignment probabilities
  - marginal_probs_[0].pdf: Plot of marginal individual assignment probabilities. One file will be created for every tuple length to assign
