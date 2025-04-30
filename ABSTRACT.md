
Artifact for the paper #20: "Relational Hoare Logic for Realistically Modelled Machine Code", submitted to CAV25.

We provide two archives with the same artifact, one for amd64 and one for arm64 architecture. The compressed archive includes a docker image, the Dockerfile, the license file LICENSE.md, and README.md with the instructions to build and run the artifact in the chosen architecture. The docker image includes the [HOL Light](https://github.com/jrh13/hol-light) theorem prover and a fork of the [s2n-bignum](https://github.com/awslabs/s2n-bignum) repository (called 'hol-bignum' in the paper) containing the proof suite presented in the paper.

- Zenodo DOI, updated after the smoke-test: [10.5281/zenodo.15308819](https://doi.org/10.5281/zenodo.15308819).
- amd64 SHA256 checksum: `cb8628c30f3d8ef9109242c8f9a62b403e45ce04125e2eebb7eb54e5d64f6bd3  s2n-bignum-amd64.zip`
- arm64 SHA256 checksum: `d7c645694b0bc6f3c896b9c99e37bd5519e8df8382ec7d30d6051154bac97111  s2n-bignum-arm64.zip`
- We claim all badges: available, functional, reusable.
- We tested the artifact on both amd64 and arm64 architectures. No special requirements for Linux but we suggest Mac users to increase the memory limit to 24GB (see README.md on how to increase docker memory limit).
- Overall, testing the functional badge took 2 hours and for the reusable badge about 10 minutes.

## Update After the Smoke Test

We thank the Reviewers for their feedback. We have updated our submission with the amd64 image, and renamed the original one to `s2n-bignum-arm64.zip`. The README.md file inside both archives has been updated accordingly. Minor: the tag of the docker image is now `s2n-bignum-amd64:latest` for the amd64 image and `s2n-bignum-arm64:latest` for the arm64 image.
