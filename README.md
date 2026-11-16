# CloudPilot legacy Helm chart archive

This organization Pages site preserves the existing Helm repository URL while
the Karpenter GCP source repository moves to its new organization:

```sh
helm repo add karpenter-gcp https://cloudpilot-ai.github.io/karpenter-provider-gcp/
helm repo update karpenter-gcp
helm pull karpenter-gcp/karpenter --version 0.8.0
```

The snapshot was captured on 2026-11-16. It contains 14 `karpenter` versions and
10 `karpenter-crd` versions, up to and including 0.8.0. Chart archives and the
Helm index are copied without repackaging. SHA-256 digests were checked against
the original index. Both 0.8.0 provenance files, the public signing key, the
signed chart history, and Artifact Hub metadata are retained.

New releases are maintained by the upstream project. This archive does not
publish new chart versions.

## Publishing

GitHub Pages publishes the `main` branch from the repository root. `.nojekyll`
keeps the static files from being processed by Jekyll. No custom domain is set.

Files inside `karpenter-provider-gcp/` map to the existing Helm URL. While the
original project Pages deployment is active, it serves that path. After the
source repository moves, verify that the organization site serves the archived
files at the same URL. Repository transfer and source workflow updates are
separate from this archive.

Keep the original repository location vacant to preserve GitHub's repository
redirect. Do not recreate `cloudpilot-ai/karpenter-provider-gcp` after transfer.

## Integrity

Verify all archived files locally:

```sh
cd karpenter-provider-gcp
sha256sum --check SHA256SUMS
```

Verify the signed releases with Helm:

```sh
gpg --dearmor --output /tmp/karpenter-gcp-public.gpg \
  keys/7D575660AC2C6650E263439577A23E34D5FE007A.asc
helm verify karpenter-0.8.0.tgz --keyring /tmp/karpenter-gcp-public.gpg
helm verify karpenter-crd-0.8.0.tgz --keyring /tmp/karpenter-gcp-public.gpg
```

Keep existing packages, provenance files, public keys, URLs, and index entries
unchanged. Decide and announce a retention deadline before removing the site.
