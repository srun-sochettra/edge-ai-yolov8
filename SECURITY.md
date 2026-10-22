# Security and camera-data guidance

These are local workshop scripts, not a hardened monitoring service. This policy does not promise supported release lines, response deadlines or a security audit.

## Camera data and outputs

Use a camera only with appropriate permission. The ROI lab can save annotated snapshots; analytics scripts write timestamped CSV records. Review images and logs before sharing, limit access to retained files and remove recordings when no longer needed.

Existing ignore rules exclude models, logs and outputs inside the workspace. They do not remove files already tracked in Git or protect files copied elsewhere. Do not include recordings, private paths or identifying diagnostics in public reports.

Tracker IDs are not verified personal identities. Detection counts and alerts are estimates; do not use these exercises as the sole basis for safety-critical decisions or assessments of individuals.

## Model and dependency trust

Obtain model files from a source you trust and review the terms that apply to them. Do not load unknown model artefacts merely because they have an expected filename. Review dependency changes and the installed environment before executing scripts.

The supplied source does not establish access controls, retention enforcement, authenticated remote access or secure deployment infrastructure. No such guarantee is made by this documentation.

## Reporting

For a non-sensitive defect, provide the affected script, environment, minimal reproduction and expected/observed result. For sensitive concerns, request a private contact from the maintainer without publishing private data or exploit details. No dedicated reporting address or enabled private-reporting feature is confirmed by the supplied repository.
