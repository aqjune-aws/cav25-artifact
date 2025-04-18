
Artifact for the paper #20: "Relational Hoare Logic for Realistically Modelled Machine Code", submitted to CAV25.

The docker image includes the [HOL Light](https://github.com/jrh13/hol-light) theorem prover and a fork of the [s2n-bignum](https://github.com/awslabs/s2n-bignum) repository (called 'hol-bignum' in the paper) containing the proof suite presented in the paper.
We provide detailed instructions inside README.md to load the docker image, evaluate all badges, and to confirm that the size of the work matches the numbers we reported.

- Zenodo DOI: [10.5281/zenodo.15210623](https://doi.org/10.5281/zenodo.15210623).
- SHA256 checksum: `c595821c2b8e525e9bb81b98cb2714cd8a09bd8b7e04f9a76fe29120e9a24b4f  s2n-bignum.zip`
- We claim all badges: available, functional, reusable.
- We tested the artifact on Linux machine and Mac. No special requirements for Linux users but we suggest Mac users to increase the memory limit to 24GB (see README.md on how to increase docker memory limit).
- **We suggest Mac users to try out the Functional evaluation during the smoke-test phase to catch any potential issues with the memory limit sooner.**
- On our Linux machine, the smoke-test phase took 5 minutes, testing the functional badge took 2 hours, and for the reusable one about 10 minutes.
