# CAV25 Artifact: s2n-bignum

Artifact documentation for the paper #20: "Relational Hoare Logic for Realistically Modelled Machine Code", submitted to CAV25.
Here we provide the instructions to verify all proofs presented in Section 7, and to confirm that the size of the work matches the numbers we reported.
Optionally, we provide the instructions to run the rest of non-relational proofs.

The artifact is a docker image containing HOL Light and a fork of the s2n-bignum repository (called 'hol-bignum' in the paper for anonymicity) containing the proof suite presented in the paper.
The artifact is available at [https://doi.org/XX.XXXX/zenodo.XXXXXXXX](https://doi.org/XX.XXXX/zenodo.XXXXXXXX).
We do not require any large amount of system resources to run the artifact, we tested it on AArch64 Linux and Mac laptops.

We claim all three badges: available, functional, and reusable.

## Smoke-Test Phase

The correct behaviour of the artifcat can be evaluated by loading the docker image and running the tutorial of s2n-bignum:

1. Load and enter the provided docker image (<1 min):

    ```bash
    docker load < s2n-bignum.tar
    docker run -it cav25-trial:7.0 /bin/bash
    ```

1. Run the tutorial (~5 min):

    ```bash
    cd s2n-bignum/arm
    make tutorial -j
    ```

1. The expected result is: it will not have any line including 'Failure' or 'Exception:',
and has the running time printed at the end of the file.

    ```bash
    XXX
    ```

## Available Badge

The artifact is available on Zenodo: [https://doi.org/XX.XXXX/zenodo.XXXXXXXX](https://doi.org/XX.XXXX/zenodo.XXXXXXXX).

## Functional Badge (~XXX minutes)

The evaluation for the Functional Badge consists of loading and running the artifact on the realtional proofs presented in Section 7.

1. Load and enter the provided docker image (<1 min):

    ```bash
    docker load < s2n-bignum.tar
    docker run -it cav25-trial:7.0 /bin/bash
    ```

1. Run the proofs of Section 7 (~XXX min):

    ```bash
    cd s2n-bignum/arm
    make proofs-cav25 -j
    ```

    By running the benchmark above, 19 proofs are machine checked:

    - 4 constant-time proofs, where 3 are different styles of proofs of `bignum_copy` and 1 is the proof of `bignum_inv_p25519`.
    - 15 program equivalence proofs.

    You can find these proofs at:

    - XXX
    - XXX
    - XXX
    - XXX
    - XXX

1. The expected results is:

    ```bash
    XXX
    ```

    From the output `*.correct` files, you will be able to find the lines that starts with `(CAV25)`
    followed by the proven theorems for constant-time properties or program equivalences.

1. (Optionally) We added a few more equivalence proofs for the x86 architecture after the paper submission, you can run these with (~XXX min):

    ```bash
    cd s2n-bignum/x86
    make tutorial
    ```

1. (Optionally) Run the whole s2n-bignum with both relational and non-relational proofs (~XXX hours):

    ```bash
    cd s2n-bignum/arm
    make proofs
    ```

## Reusable Badge

To confirm the Reusable Badge, check the following:

- s2n-bignum is open-source and distributed under Apache-2.0 or ISC or MIT-0 (see `./LICENSE.md`), which allow reuse and repurposing.
- s2n-bignum only depends on HOL Light (which indirectly depends on OCaml) and the usual disassembly suite (e.g., `as`). We provide makefiles to help building the tool and verify the proofs (see `./x86/Makefile`).
- We encourage reviewers to try the tutorials in `./tutorial`.
- To confirm the size of our work, run:
  - `XXX` for the size of the whole s2n-bignum (expected: XXX)
  - `XXX` for the size of the constant-time proofs (expected: XXX)
  - `XXX` for the size of the equivalence proofs (expected: XXX)
  - `XXX` for the size of the relational framework (expected: XXX)
- To use s2n-bignum outside the artifact refer to the instructions at [https://github.com/awslabs/s2n-bignum/tree/main](https://github.com/awslabs/s2n-bignum).
- The code is well written and documented, important files are (you can open files with `vi <filename>`, show line numbers with `:set number`, and goto a specific line with `:line_number`):
  - `s2n-bignum/common/relational_n.ml`
    - line 155: Definition 3 (Stronger Eventually), page 6
    - line 171: Conjunction rule, page 7
    - line 268: Lemma 1, page 7
    - line 350: Definition 4 (Stronger Ensures), page 7
    - line 363: Theorem 1, page 8
    - line 394: Theorem 2, page 8
  - `s2n-bignum/common/relational2.ml`
    - line 22: Definition 5 (Relational Ensures), page 8
    - line 249: Commutativity rule, page 7
    - line 256: Composition rule, page 7
    - line 358: Lemma 2 (Commutativity), page 9
    - line 393: Lemma 3 (Compositional), page 9 (typo in the paper: the step function in the rule should be n0 + n1 and m0 + m1 as in the repo. We will fix the paper)
    - line 515: Lemma 4 (Compositional of Frame Conditions), page 9
    - line 495: Lemma 5 (Conjunction), page 9
    - line 329: Definition 6 (Hybrid Ensures 2), page 10 (Note that, the repo does not provide an explicit definition of "Hybrid Ensures 2", instead it matches the precondition of Theorem 4)
    - line 329: Theorem 4, page 10
    - line 349: Theorem 3, page 10
  - `s2n-bignum/XXX`
    - line XXX: Definition 7 (Constant-Time via Event Accumulation), page 12
    - line XXX: Definition 8 (Constant-Time via Unary to Relational Embedding), page 13
  - `s2n-bignum/common/equiv.ml`
    - line XXX: Definition 9 (Equivalence), page 14
    - line XXX: Theorem 5 (Transfer of Correctness through Equality), page 15
  - `s2n-bignum/arm/proofs/equiv.ml`

## Artifact Notes

This artifact has been compiled with `docker build -t s2n-bignum .` (~10 min) on a linux machine and saved with `docker save s2n-bignum > s2n-bignum.tar` (<1 min).
