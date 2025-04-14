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

1. Load and enter the provided docker image:
```bash
docker load < s2n-bignum.tar
docker run -it cav25-trial:7.0 /bin/bash
```

2. Run the tutorial (~5 min):
```bash
cd $HOME/arm
make tutorial -j
```

3. The expected result is: it will not have any line including 'Failure' or 'Exception:',
and has the running time printed at the end of the file.
```bash
XXX
```

## Available Badge

The artifact is available on Zenodo: [https://doi.org/XX.XXXX/zenodo.XXXXXXXX](https://doi.org/XX.XXXX/zenodo.XXXXXXXX).

## Functional Badge (~XXX minutes)

The evaluation for the Functional Badge consists of loading and running the artifact on the realtional proofs presented in Section 7.

1. Load and enter the provided docker image:
```bash
docker load < s2n-bignum.tar
docker run -it cav25-trial:7.0 /bin/bash
```

2. Run the proofs of Section 7 (~XXX min):
```bash
cd $HOME/arm
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

3. The expected results is:
```bash
XXX
```

From the output `*.correct` files, you will be able to find the lines that starts with `(CAV25)`
followed by the proven theorems for constant-time properties or program equivalences.

4. (Optionally) We added a few more equivalence proofs for the x86 architecture after the paper submission, you can run these with (~XXX min):
```bash
cd $HOME/x86
make tutorial
```

5. (Optionally) Run the whole s2n-bignum with both relational and non-relational proofs (~XXX hours):
```bash
cd $HOME/arm
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
- The code is well written and documented, important files are:
  - `XXX`
  - `XXX`
  - `XXX`

## Artifact Notes

This artifact has been compiled with `docker build -t s2n-bignum .` (~15 min) in a linux machine and saved with `docker save s2n-bignum > s2n-bignum.tar` (~1 min).

