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
  string                       chain_id             = 2;
  int64                        height               = 3;
  google.protobuf.Timestamp    time                 = 4;
  BlockID                      last_block_id        = 5;
  bytes                        last_commit_hash     = 6;
  bytes                        data_hash            = 7;
  bytes                        validators_hash      = 8;
  bytes                        next_validators_hash = 9;
  bytes                        consensus_hash       = 10;
  bytes                        app_hash             = 11;
  bytes                        last_results_hash    = 12;
  bytes                        evidence_hash        = 13;
  bytes                        proposer_address     = 14;
}
```

```proto
message Data {
  repeated bytes txs = 1;
}
```

```proto
message Commit {
  int64              height     = 1;
  int32              round      = 2;
  BlockID            block_id   = 3;
  repeated CommitSig signatures = 4;
}
```

```proto
message CommitSig {
  BlockIDFlag               block_id_flag     = 1;
  bytes                     validator_address = 2;
  google.protobuf.Timestamp timestamp         = 3;
  bytes                     signature         = 4;
}
```

## Discussion

* TODO

## References

* TODO
