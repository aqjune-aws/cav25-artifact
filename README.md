# CAV25 Artifact: s2n-bignum

Artifact documentation for the paper #20: "Relational Hoare Logic for Realistically Modelled Machine Code", submitted to CAV25.
Here we provide the instructions to verify all proofs presented in Section 7, and to confirm that the size of the work matches the numbers we reported.
Optionally, we provide the instructions to run the rest of non-relational proofs.


The artifact is a docker image containing [HOL Light](https://github.com/jrh13/hol-light) and a clone of the [s2n-bignum](https://github.com/awslabs/s2n-bignum) repository (called 'hol-bignum' in the paper for anonymity) containing the proof suite presented in the paper.
The cloned s2n-bignum directory is a result of cloning https://github.com/awslabs/s2n-bignum and applying a patch that
(1) adds constant time proofs that are not available in the mainstream yet, and (2) updating the existing equivalence checking proofs to explicitly print the equivalence theorems for artifact evaluation.
The artifact is available on Zenodo at [10.5281/zenodo.15210623](https://doi.org/10.5281/zenodo.15210623).

We tested the artifact on AArch64 Linux and Mac.
> No special requirement for Linux but we suggest Mac users to increase docker resources: Docker Desktop > Settings > Resources > Advanced > Memory limit: 24GB, Swap 4GB, CPU limit: 12. On Mac with 12 cores we estimate an usage of ~20 GB of memory when 12 proofs run in parallel. Decrease the available CPUs in the make scripts (via the `-j` parameter, e.g., `-j2` for only 2 CPUs) if you cannot allocate that much memory.

We claim all three badges: available, functional, and reusable. In the following, we first provide the instructions to run the smoke-test phase, then the evaluation for each badge (available, functional, and reusable) with their expected running time and results.

## Smoke-Test Phase (~5 minutes)

The correct behavior of the artifact can be evaluated by loading the docker image and running the tutorial of s2n-bignum:

1. Load and enter the provided docker image (<1 min):

    ```bash
    docker load < s2n-bignum.tar
    docker run -it cav25-trial:7.0 /bin/bash
    ```

2. Run the tutorial (~5 min):

    ```bash
    cd s2n-bignum/arm
    make tutorial -j
    ```

    > Mac users: if the script fails, it is probably due to out of memory. You can try to run the script with `make tutorial -j2` or `make tutorial` (it will take longer, though).

3. The script should generate `*.correct` logs in `arm/tutorial/` for each `*.ml` proof file. Some warnings are expected, but the script should not fail.

    Each `*.correct` file should end with the running time, e.g.:

    ```bash
    tail -n 1 tutorial/rel_equivtac.correct
    Running time: 26.000000 sec, Start unixtime: 1744637734.000000, End unixtime: 1744637760.000000
    ```

    If an error occurred, the `*.correct` file will contain the keyword 'Failure' or 'Exception'. Make sure none of the `*.correct` files contain these keywords:

    ```bash
    grep -F 'Failure' tutorial/*.correct
    grep -F 'Exception' tutorial/*.correct
    ```

4. For Mac users:

   > We suggest Mac users to run the Functional Badge evaluation during the smoke-test phase to catch any potential issues with the memory limit sooner. If you run into memory issues, you can try to run the script with `make proofs-cav25 -j2` or `make proofs-cav25` (it will take much longer, though), or increase docker memory limit as explained above.

## Available Badge

The artifact is available on Zenodo at [10.5281/zenodo.15210623](https://doi.org/10.5281/zenodo.15210623).

## Functional Badge (~2 hours)

The evaluation for the Functional Badge consists of loading and running the artifact on the relational proofs presented in Section 7.

1. Load and enter the provided docker image (<1 min):

    ```bash
    docker load < s2n-bignum.tar
    docker run -it cav25-trial:7.0 /bin/bash
    ```

2. Run the proofs of Section 7 (~2 hours):

    ```bash
    cd s2n-bignum/arm
    make proofs-cav25 -j
    ```

    > Mac users: as for the tutorial, try `make proofs-cav25 -j2` if any error occurs. Execution time may take many more hours without multi-threading.

    By running the benchmark above, 19 proofs are machine checked:

    - 4 constant-time proofs, where 3 are different styles of proofs of `bignum_copy` and 1 is the proof of `bignum_inv_p25519`.
    - 15 program equivalence proofs.

    You can find these proofs at:

    - `./s2n-bignum/arm/proofs/bignum_inv_p25519.fn_and_const_combined.ml`
    - `./s2n-bignum/arm/proofs/bignum_copy.constant_time_ensures_n.ml`
    - `./s2n-bignum/arm/proofs/bignum_copy.fn_and_const_combined.ml`
    - `./s2n-bignum/arm/proofs/bignum_copy.constant_time_ensures2.ml`
    - `./s2n-bignum/arm/proofs/bignum_mul_8_16.ml`
    - `./s2n-bignum/arm/proofs/bignum_sqr_8_16.ml`
    - `./s2n-bignum/arm/proofs/bignum_emontredc_8n_cdiff.ml`
    - `./s2n-bignum/arm/proofs/bignum_montmul_p256.ml`
    - `./s2n-bignum/arm/proofs/bignum_montmul_p384.ml`
    - `./s2n-bignum/arm/proofs/bignum_montmul_p521.ml`
    - `./s2n-bignum/arm/proofs/bignum_montsqr_p256.ml`
    - `./s2n-bignum/arm/proofs/bignum_montsqr_p384.ml`
    - `./s2n-bignum/arm/proofs/bignum_montsqr_p521.ml`
    - `./s2n-bignum/arm/proofs/bignum_mul_p521.ml`
    - `./s2n-bignum/arm/proofs/bignum_sqr_p521.ml`
    - `./s2n-bignum/arm/proofs/p256_montjadd.ml`
    - `./s2n-bignum/arm/proofs/p256_montjdouble.ml`
    - `./s2n-bignum/arm/proofs/p384_montjadd.ml`
    - `./s2n-bignum/arm/proofs/p384_montjdouble.ml`

3. As for the smoke-test phase, check the expected result by the lack of failures during the script execution:

    ```bash
    grep -F 'Failure' **/*.correct
    grep -F 'Exception' **/*.correct
    ```

    From the output `*.correct` files, the lines starting with "(CAV25)" describes the proofs that were run (expect more than 19 entries as the same theorem can be tested multiple times with different parameters):

    ```bash
    grep -F '(CAV25)' **/*.correct
    ```

4. (Optional) Run the whole s2n-bignum with both relational and non-relational proofs that are already checked in the s2n-bignum mainstream (~5 hours). This will not include constant-time proofs since they are not in the mainstream yet.

    ```bash
    cd ../arm
    make proofs -j
    ```

## Reusable Badge (~10 minutes)

To confirm the Reusable Badge, check the following:

- s2n-bignum is open-source and distributed under Apache-2.0, ISC or MIT-0 (see `LICENSE.md` in Zenodo or `./s2n-bignum/LICENSE`), which allow reuse and repurposing.
- s2n-bignum only depends on HOL Light (which indirectly depends on OCaml) and the usual disassembly suite (e.g., `as`). We provide makefiles to help building the tool and verify the proofs (e.g., `./s2n-bignum/arm/Makefile`). To build and use s2n-bignum outside the artifact refer to the instructions at [github.com/awslabs/s2n-bignum](https://github.com/awslabs/s2n-bignum/tree/main)
- We encourage reviewers to try the tutorials in `./s2n-bignum/arm/tutorial`.
- To confirm the size of our work, run (note that the paper may not report the exact same numbers as the ones below as s2n-bignum is under active development and we performed a patch and rebase to create the artifact, we will update the camera-ready version of the paper with these numbers):
  - `cloc ./s2n-bignum/common --by-file --not-match-f '^(relational2\.ml|relational_n\.ml)$'` for the size of the non-relational part of s2n-bignum (expected: ~10k LOC, referenced at page 6 of the paper)
  - `cloc ./s2n-bignum/common/relational2.ml s2n-bignum/common/relational_n.ml` for the size of the relational framework (expected: 1630 LOC, referenced at page 9 of the paper)
  - `cloc . --by-file --match-f '^(bignum_inv_p25519.fn_and_const_combined\.ml|bignum_copy\.constant_time_ensures2\.ml|bignum_copy\.constant_time_ensures_n\.ml|bignum_copy\.fn_and_const_combined\.ml)$'` for the size of the constant-time proofs (expected: 4293 LOC, referenced at page 16 of the paper)
  - `cloc --by-file */proofs/equiv.ml` for the size of the equivalence framework (expected: 2452 LOC, referenced at page 16 of the paper)
  - `cloc ./s2n-bignum/arm/proofs --by-file --match-f '^(bignum_mul_8_16\.ml|bignum_sqr_8_16\.ml|bignum_emontredc_8n_cdiff\.ml|bignum_montmul_p256\.ml|bignum_montmul_p384\.ml|bignum_montmul_p521\.ml|bignum_montsqr_p256\.ml|bignum_montsqr_p384\.ml|bignum_montsqr_p521\.ml|bignum_mul_p521\.ml|bignum_sqr_p521\.ml|p256_montjadd\.ml|p256_montjdouble\.ml|p384_montjadd\.ml|p384_montjdouble\.ml)$'` for the size of equivalence proofs (expected 33k LOC, referenced at page 17 of the paper)
  - `cloc ./s2n-bignum --include-lang=OCaml` for the whole s2n-bignum proofs (expected: 890k LOC, referenced at page 6 of the paper)
- The code is well written and documented, important files are (you can open files with `vi <filename>`, show line numbers with `:set number`, and goto a specific line with `:line_number`):
  - `./s2n-bignum/common/relational_n.ml`
    - line 155: Definition 3 (Stronger Eventually), page 6 of the paper
    - line 171: Conjunction rule, page 7 of the paper
    - line 268: Lemma 1, page 7 of the paper
    - line 350: Definition 4 (Stronger Ensures), page 7 of the paper
    - line 363: Theorem 1, page 8 of the paper
    - line 394: Theorem 2, page 8 of the paper
  - `./s2n-bignum/common/relational2.ml`
    - line 22: Definition 5 (Relational Ensures), page 8 of the paper
    - line 249: Commutativity rule, page 7 of the paper
    - line 256: Composition rule, page 7 of the paper
    - line 329: Definition 6 (Hybrid Ensures 2), page 10 (Note that, the repo does not provide an explicit definition of "Hybrid Ensures 2", instead it matches the precondition of Theorem 4) of the paper
    - line 329: Theorem 4, page 10 of the paper
    - line 349: Theorem 3, page 10 of the paper
    - line 358: Lemma 2 (Commutativity), page 9 of the paper
    - line 393: Lemma 3 (Compositional), page 9 of the paper (typo in the paper: the step function in the rule should be n0 + n1 and m0 + m1 as in the repo. We will fix the paper)
    - line 495: Lemma 5 (Conjunction), page 9 of the paper
    - line 515: Lemma 4 (Compositional of Frame Conditions), page 9 of the paper
  - To build and use s2n-bignum outside the artifact refer to the instructions at [github.com/awslabs/s2n-bignum](https://github.com/awslabs/s2n-bignum/tree/main).

## Changelog & Notes

s2n-bignum is under active development, during the last few months we have added some equivalence proofs for the x86 architecture and other minor changes:

- previously conditional branch event was only taking one parameter (true/false, for taken/not taken); but now it is taking a pair of (current PC, next PC). This is to support return instruction.
- load/store are having one additional natural number parameter, which is the access size.
- size of constant-time proofs is slightly bigger.

> We will update the paper to reflect these changes for the camera-ready version.

This artifact has been compiled with `docker build -t cav25-trial:7.0 .` (~10 min) on a Linux machine and saved with `docker save cav25-trial:7.0 > s2n-bignum.tar` (<1 min). The docker image is ~2.6GB
