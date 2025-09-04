# Operations

These are the things you can _do_ with snapshots:

1. **Create a Snapshot**
   * From an existing EBS volume, or automatically via AMI creation.
   * Crash-consistent by default (application-consistent requires extra steps).
2. **Copy a Snapshot**
   * To another Region (for DR).
   * To another KMS key (re-encrypt with new CMK).
   * Cross-account by sharing and copying.
3. **Create Volume from Snapshot**
   * Use snapshot as a template to create new EBS volumes.
   * Multiple volumes can be created in parallel.
4. **Register as AMI**
   * Snapshots form the root device for an AMI.
   * Required for launching EC2 instances.
5. **Share Snapshot**
   * With specific AWS accounts (private).
   * Publicly (caution: security risk).
   * Encrypted snapshots require sharing the CMK.
6. **Delete Snapshot**
   * Frees up storage space.
   * AWS preserves any blocks still referenced by later snapshots.
   * If Recycle Bin is enabled, snapshot goes there first.
