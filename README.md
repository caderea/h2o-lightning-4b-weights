# H2O Lightning 4B weights mirror

GitHub Releases mirror of the [h2oai/h2o-lightning-4b](https://huggingface.co/h2oai/h2o-lightning-4b) Hugging Face snapshot. Independent of H2O.ai.

**The Git repository contains scripts, not model weights.** The full upstream file snapshot (including model files and relevant licenses/notices) is packaged into approximately 1 GiB numbered ZIP chunks and published as GitHub Release assets. The Release manifest records the exact upstream commit and SHA-256 checksums.

## Publish the weights from GitHub Actions

Open [Publish H2O Lightning 4B weights](https://github.com/caderea/h2o-lightning-4b-weights/actions/workflows/publish-weights.yml), select **Run workflow** on `main`, and use the default tag `h2o-lightning-4b-v1` and revision `main`. The publisher resolves `main` to an immutable upstream commit SHA, streams files into ZIP chunks, uploads each completed chunk, deletes the temporary local part, and publishes the Release **only when all parts and `manifest.json` have uploaded**.

Failed uploads remain drafts. Running a **new workflow** with the same tag and same resolved upstream revision can reuse the existing chunks, provided size and SHA-256 hashes match. A resumed upload rejects inconsistent chunks rather than silently overwriting them. Large upstream downloads also support HTTP Range resumption after transient network errors.

If upstream access requires a token, put an authorized `HF_TOKEN` in the repository's GitHub Actions secrets. Never commit credentials.

## Download on another computer (no Hugging Face CLI needed)

Requires Git and Python 3.10+.

```bash
git clone https://github.com/caderea/h2o-lightning-4b-weights.git
cd h2o-lightning-4b-weights

python3 scripts/weights.py download \
  --tag h2o-lightning-4b-v1 \
  --out ./models/h2o-lightning-4b
```

The downloader fetches Release assets directly from GitHub, verifies each part, reassembles the archive, extracts all files, and checks every file against `manifest.json`. Valid downloaded parts are cached to support interrupted downloads.

**Download will only work once the Release is published.** The downloader needs extra free disk space for cached chunks, the temporary assembled ZIP and extracted weights. Running inference requires additional runtime dependencies and compatible hardware; this script only retrieves original model files.

## Model provenance and license

Original model: https://huggingface.co/h2oai/h2o-lightning-4b

Review and comply with the license and any other usage terms in the upstream repository. Retain all upstream LICENSE / NOTICE attribution files. GitHub mirror redistribution does not imply H2O.ai's endorsement.

The immutable upstream revision and every original file hash can be inspected in the published `manifest.json`.
