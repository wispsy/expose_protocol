# Expose Protocol 0.1.1 qualification

This patch publishes the Wispsy bundle identity with compatibility for generated
0.1.0 apps. Inspection accepts only the exact current or legacy hash-derived
identifier for the manifest scheme. Installation receipts must match the actual
app identifier. Existing managed handlers can be replaced or removed; unrelated
handlers still require explicit takeover, and failed replacement restores the
old app, receipt and selected handler.

Run `uv build --out-dir dist`, `python scripts/check_release.py dist --tag
v0.1.1`, and `python scripts/check_distribution.py dist` on Python 3.14.
The last command installs both selected artifacts into independent environments
outside the checkout and tests URL/argv handling, entry points, examples and
managed lifecycle contracts. On macOS it builds a temporary app and checks its
isolated launcher. Native registration/removal is tested only on disposable
macOS CI runners using the existing explicit lifecycle flag.

Merge the passing Linux/macOS checks before publishing. `release.yaml` uses
environment `pypi` and Trusted Publishing, uploads the exact qualified pair and
retains its hashes. Confirm actual PyPI files and an index installation before
recording publication as complete. No persistent local URL registration or
service deployment is part of this release preparation.
