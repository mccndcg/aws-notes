# whys

## Corruption

{% hint style="warning" %}
okay, if it is incremental, and there are 5 snapshots saved, what will happen if i delete the 3rd? will it corrupt the 4th and 5th?
{% endhint %}

#### How Incremental Snapshots Work

* Each snapshot after the first only saves the blocks that have changed since the **previous snapshot**.
* But — each snapshot is a **self-contained view** of the volume at the time it was taken. AWS handles the block mapping behind the scenes.

***

#### What Happens If You Delete Snapshot #3 (out of 5)

* AWS checks which blocks in snapshot #3 are **still needed** by later snapshots (#4 and #5).
* If a block is needed, AWS automatically preserves it by associating it with a later snapshot.
* Then snapshot #3 is deleted as a reference point.

Result:

* Snapshots #4 and #5 remain intact and usable.
* You lose nothing — AWS re-maps the block references as needed.
* Only the unique, unreferenced data blocks in snapshot #3 are actually removed from storage.

***

### Flow

```mermaid
flowchart TD

subgraph Before_Deletion
    S1[Snapshot #1<br/>Blocks: A B C D]
    S2[Snapshot #2<br/>Blocks: B' D']
    S3[Snapshot #3<br/>Blocks: A']
    S4[Snapshot #4<br/>Blocks: C']
    S5[Snapshot #5<br/>Blocks: D'']
    
    S1 --> S2
    S2 --> S3
    S3 --> S4
    S4 --> S5
end

subgraph After_Deletion
    S1a[Snapshot #1<br/>Blocks: A B C D]
    S2a[Snapshot #2<br/>Blocks: B' D']
    S4a[Snapshot #4<br/>Blocks: C' + A' -kept-]
    S5a[Snapshot #5<br/>Blocks: D'' + A' -kept-]
    
    S1a --> S2a
    S2a --> S4a
    S4a --> S5a
end

S3 -. Deleted, blocks re-linked .-> S4a

```

### Exam Tip

* Deleting a snapshot **does not corrupt the snapshot chain**.
* Every snapshot is a complete, restorable volume, regardless of whether earlier snapshots still exist.
* The only effect is on storage cost: blocks unique to the deleted snapshot are freed.
