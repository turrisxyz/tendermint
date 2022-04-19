# RFC 019: 

## Changelog

- 19-Apr-2022: Initial draft (@williambanfield).

## Abstract

* TODO

## Background

### Current Block Structure

The current block structure is included here to aid discussion.

```proto
message Block {
  Header                        header      = 1;
  Data                          data        = 2;
  tendermint.types.EvidenceList evidence    = 3;
  Commit                        last_commit = 4;
}
```

```proto
message Header {
  tendermint.version.Consensus version              = 1;
  // does this need to be here at all?
  string                       chain_id             = 2;


  int64                        height               = 3;



  google.protobuf.Timestamp    time                 = 4;


  BlockID                      last_block_id        = 5;


  bytes                        last_commit_hash     = 6;


  bytes                        data_hash            = 7;

  // Do both of these need to be included here?
  bytes                        validators_hash      = 8;
  bytes                        next_validators_hash = 9;
  // what is this, oh yeah the hash of the consensus params.
  // ugh.
  bytes                        consensus_hash       = 10;
  bytes                        app_hash             = 11;
  // What is the use of this?
  bytes                        last_results_hash    = 12;
  // Does this need to be kept separately?
  bytes                        evidence_hash        = 13;
  // This is not accurate, what if we changed to POL round.
  bytes                        proposer_address     = 14;
  // why not just have a 'fields hash' that's the hash of all of the
  // fields in the block?
}
```

```proto
message Data {
  repeated bytes txs = 1;
}
```

```proto
message Commit {
  // Why is this needed here at all? Gossip and storage maybe?
  int64              height     = 1;
  // can this instead be contained in the header? Not sure why this is here either
  // Ah, it contains information that will have been signed by the committers.
  int32              round      = 2;
  // Can definitely 
  BlockID            block_id   = 3;
  repeated CommitSig signatures = 4;
}
```

```proto
message CommitSig {
  // remove
  BlockIDFlag               block_id_flag     = 1;
  // If the list is in order, I'm not sure this needs to be in the block
  // at all.
  bytes                     validator_address = 2;
  // remove
  google.protobuf.Timestamp timestamp         = 3;
  bytes                     signature         = 4;
}
```

```proto
message BlockID {
  bytes         hash            = 1;

  // remove
  PartSetHeader part_set_header = 2; // Q Do we ever use the PartSetHeader from the actual block header to rebuild the block or figure out what to grab?
}
```

### What is the goal of this project?

Remove as much as possible from the block so that:

1. ABCI can still receive enough information to function.
2. Light clients can quickly prove the state of the blockchain. #REWORD
3. Nodes performing blocksync to catchup can restore state and verify that
consensus proceeded correctly using only the contents of the block.
4. Operators and developers can debug problems that arise with the state
machine using the contents of the block.

## Discussion

* TODO

## References

* TODO
