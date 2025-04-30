
Artifact for the paper #20: "Relational Hoare Logic for Realistically Modelled Machine Code", submitted to CAV25.

We provide two docker images with the same content, one for amd64 and one for arm64 architectures. The images include the [HOL Light](https://github.com/jrh13/hol-light) theorem prover and a fork of the [s2n-bignum](https://github.com/awslabs/s2n-bignum) repository (called 'hol-bignum' in the paper) containing the proof suite presented in the paper.
We provide detailed instructions inside README.md to load the docker image in your specific architecture, evaluate all badges, and to confirm that the size of the work matches the numbers we reported.

- Zenodo DOI, updated after the smoke-test: [10.5281/zenodo.15308819](https://doi.org/10.5281/zenodo.15308819).
- amd64 SHA256 checksum: `cb8628c30f3d8ef9109242c8f9a62b403e45ce04125e2eebb7eb54e5d64f6bd3  s2n-bignum-amd64.zip`
- arm64 SHA256 checksum: `d7c645694b0bc6f3c896b9c99e37bd5519e8df8382ec7d30d6051154bac97111  s2n-bignum-arm64.zip`
- We claim all badges: available, functional, reusable.
- We tested the artifact on both amd64 and arm64 architectures. No special requirements for Linux but we suggest Mac users to increase the memory limit to 24GB (see README.md on how to increase docker memory limit).
- Overall, testing the functional badge took 2 hours and for the reusable badge about 10 minutes.
