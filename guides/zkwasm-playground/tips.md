# ZKWasm Playground Tips & Tricks

### Viewing Requests in Flight

You can use `tcpdump` to capture requests received and sent from Rest Server port:

```bash
PORT=8109 tcpdump -i lo -A -s 0 "tcp port $PORT and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12]&0xf0)>>2)) != 0)" -w capture.pcap
```

### Force Your Proving Nodes to be Certified

Only prover nodes that are certified can run proofs, the executing the following command in `MongoDB` shell will force them to be
classified as certified. Note: Your address must be in lower case.

```javascript
use zkwasmTaskDB
db.prover_nodes.updateOne({"address" : "0x...YOUR_NODE_ADDRESS_HERE"}, {$set : {"prover_level" : "Certified"}})
db.prover_nodes.updateOne({"address" : "0x...YOUR_NODE_ADDRESS_HERE"}, {$set : {"performance_track" : "0x0000000000000000000000000000000000000"}})
```

### File Upload Size Limit Privileges

Increase privileges value for easy testing context uploads. Update the `user_non_privilege_value` in the file
`src/user/privileges/values.rs` to be 4000.

`src/user/privileges/values.rs`:

```rust
 ...
 // ----------------------------- default privilege values -----------------------------

 const user_non_privilege_value: privilegevalue = privilegevalue::number(SET_THIS_VALUE_HERE);

 ...
```

### Test Subscription

Adjust subscription plans config file to your specific token address for the test network.

`subscription_plans.json`:

```json
{
   {
     "subscription_type": "Basic",
     "token_params": {
       "token_address": "$YOUR_TOKEN_ADDRESS_HERE",
       "network_id": $YOUR_NETWORK_ID_HERE
     },
     ...

     "subscription_type": "Developer",
     "token_params": {
       "token_address": "$YOUR_TOKEN_ADDRESS_HERE",
       "network_id": $YOUR_NETWORK_ID_HERE
     },
     ...
   }
}
```

### Increasing Account's Credits

Only with your user account has credits will you be able to run prove tasks. You can buy credits via the Web GUI but its much
easier to directly update your user entry in the `MongoDB`, this can be done with the following command. Note: Your address must
be in lower case.

```javascript
use zkwasmTaskDB
db.users.updateOne({user_address : "0x...YOUR_USER_ADDRESS_HERE""}, {$set: { credit_deficit: '0x0', credits: '0xFFFFFF' } })
```

There's a chance your user may not have been created yet. If so then trigger a setup task and it will be created.

### Backup and Restoring Server Data

It is important to be able to load up data from other rest servers into your own server, this is what we call backup from
existing.

The main service data that can be transferred between instances is the `MongoDB` data, `RocksDB` data and Statics data
(`server_storage/statics`).

Dumping and restoring the DB is simplified by using the
[playground mongo tool](https://github.com/ZhenXunGe/playground-mongodb-tool/blob/main/README.md#usage-1).

- Example dumping all service data
  [here](https://github.com/ZhenXunGe/playground-mongodb-tool/blob/main/README.md#backup-example).
- Example restoring all service data
  [here](https://github.com/ZhenXunGe/playground-mongodb-tool/blob/main/README.md#restore-example).

Otherwise:

- `MongoDB` is best handled via `mongodump` and `mongorestore` tools, ZKP contains bash scripts for both dumping and restoring the
  db, see documentation
  [here](https://github.com/ZhenXunGe/zkWASM-playground/tree/main?tab=readme-ov-file#dumping-and-restoring-database)
- `RocksDB` and Statics can be treated like a folder and hence can be copied and tar'd like one.

### Running Multiple Provers on the same machine

Running multiple provers can be done in the same folder as long as your give them their own address/key pair, and their own
workspace folder.

You will need to create a new directory for the prover server data (e.g. `workspace_1`), it must be unique to that prover and the
prover must be given its own `prover_config.json` with unique address/key pair.

Example:

```bash
RUST_LOG=info RUST_BACKTRACE=1 cargo run --release --features profile -- --config $UNIQUE_PROVER_CONFIG_HERE --proversystemconfig prover_system_config.json -w $UNIQUE_PROVER_WORKSPACE_HERE -s
```

Then, only the K params need to copied into the statics directory of the new workspace and all other statics will be generated.

Example:

```
mkdir -p ../proveservice/workspace_1/static && cp ./server_storage/static/K2* ../proveservice/workspace_1/static/
```

Finally, the Rest server config (`server_config.json`) must be updated to include the new prover address in `"prover_addresses"`
list.

If you prover is not picking up prove tasks then it may need to set to "Certified", see
[here](#force-your-proving-nodes-to-be-certified).
