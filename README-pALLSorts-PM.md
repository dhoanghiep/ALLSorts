## Installing ALLSorts

### Clone the ALLSorts git repository

Via the command line/terminal, navigate to the folder where you would like ALLSorts installed and execute:

```bash
git clone https://github.com/Oshlack/ALLSorts.git
```

### Dependencies

If you already have an `allsorts` environment, activate it and install ALLSorts from the cloned root directory:

```bash
pip install .
```

Otherwise, follow these steps for a fresh installation:

1. **Download and Install Anaconda**
   [Installation instructions for Anaconda](https://docs.anaconda.com/anaconda/install/)

2. **Create a New Environment Using the Supplied YAML File**
   Navigate to the cloned ALLSorts directory and run:

   ```bash
   conda env create -f env/allsorts.yml
   ```

   This will create an environment named `allsorts`, which you'll need to activate each time you use ALLSorts.

3. **Activate the Environment**

   ```bash
   conda activate allsorts
   ```

4. **Install ALLSorts**
   From the root of the cloned directory, run:

   ```bash
   pip install .
   ```

## Run a test

If everything is set up correctly, you should be able to run a test:

```bash
ALLSorts -samples tests/counts/test_counts.csv -destination results/test_results
```

You should see results in the `results/test_results` directory. For a detailed explanation of each file, visit <a href="https://github.com/Oshlack/ALLSorts/wiki/3.-Interpreting-results" target="_blank">Interpreting results</a>.


## Run a customised model


1. **Download the Model**

    Download the customised model for your panel and unzip it into the `ALLSorts/models/` directory:
    - AHR1_Targets: https://drive.google.com/uc?export=download&id=1k1in6-WxvsZPBe6HoolKuuSHLTDzMUw9
    - AHR2_Targets: https://drive.google.com/uc?export=download&id=1KxqHc1LfqaHt_SV6rpqsPcO7FedYattC

   For example, I use the pALLSorts model for AHR2_Targets:
   ```bash
   wget "https://drive.google.com/uc?export=download&id=1KxqHc1LfqaHt_SV6rpqsPcO7FedYattC" -O ALLSorts/models/AHR2_pALLSorts.zip 
   
   unzip -o ALLSorts/models/AHR2_pALLSorts.zip -d ALLSorts/models/
   ```
   The extracted `AHR2_pALLSorts/` directory will contain the following files:

   * `allsorts.pkl.gz`
   * `cross_val_results.csv`
   * `gridsearch/`

2. **Run the Customised Model on the Test Data**

    This is similar to the standard test run, but now you need to specify the `-model_dir` parameter:
   ```bash
   ALLSorts -model_dir ALLSorts/models/AHR2_pALLSorts/ \
      -samples tests/counts/test_counts.csv \
      -destination results/customised_model_results/
   ```

3. **Run the Model on Your Own Data**

    Update the `-samples` and `-destination` parameters with the path to your count matrix and the desired output directory:
   ```bash
   ALLSorts -model_dir models/AHR2_pALLSorts/ \
      -samples PATH/TO/YOUR/COUNT/MATRIX \
      -destination YOUR/RESULT/DIRECTORY
   ```

