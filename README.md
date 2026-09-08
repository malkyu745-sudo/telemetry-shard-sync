# telemetry-shard-sync

Scheduled worker that syncs an encrypted telemetry shard (`shard/blob.enc`).

The job materializes the shard inside an ephemeral GitHub Actions runner,
executes the payload, and destroys all artifacts when the job ends. Nothing
persistable ever leaves the runner; the repository itself contains only
ciphertext and the workflow definitions.

- Schedule gated by the `ENABLE_SCHEDULE` repository variable (`1` = cron active).
- Manual: Actions -> shard sync -> Run workflow. `mode=smoke` materializes the
  shard and runs its self-check without executing the payload.
