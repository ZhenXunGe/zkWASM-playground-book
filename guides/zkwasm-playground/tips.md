# ZKWasm Playground Tips & Tricks

### Viewing Requests in Flight

You can use `tcpdump` to capture requests received and sent from Rest Server port:

```
PORT=8109 tcpdump -i lo -A -s 0 "tcp port $PORT and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12]&0xf0)>>2)) != 0)" -w capture.pcap
```

### Force Your Proving Nodes to be Certified

Only prover nodes that are certified can run proofs, the executing the following command in `MongoDB` shell will force them to be classified as
certified.
Note: Your address must be in lower case.

```
use zkwasmTaskDB
db.prover_nodes.updateOne({"address" : "0x...YOUR_NODE_ADDRESS_HERE"}, {$set : {"prover_level" : "Certified"}})
db.prover_nodes.updateOne({"address" : "0x...YOUR_NODE_ADDRESS_HERE"}, {$set : {"performance_track" : "0x0000000000000000000000000000000000000"}})
```

### File Upload Size Limit Privileges 

Increase privileges value for easy testing context uploads
```
diff --git a/src/user/privileges/values.rs b/src/user/privileges/values.rs
index 6da0f1d9..d709ab71 100644
--- a/src/user/privileges/values.rs
+++ b/src/user/privileges/values.rs
@@ -54,7 +54,7 @@ impl privilegevalue {

 // ----------------------------- default privilege values -----------------------------

-const user_non_privilege_value: privilegevalue = privilegevalue::number(0);
+const user_non_privilege_value: privilegevalue = privilegevalue::number(4000);

 // ------------------------------------------------------------------------------------
```

### Test Subscription

Adjust subscription plans

`subscription_plans.json`
```
diff --git a/subscription_plans.json b/subscription_plans.json
index f989301b..3d11e4e0 100644
--- a/subscription_plans.json
+++ b/subscription_plans.json
@@ -2,8 +2,8 @@
   {
     "subscription_type": "Basic",
     "token_params": {
-      "token_address": "0xa8d3dee6671c4fdac4743a1eb1F276EabD4ba302",
-      "network_id": 56
+      "token_address": "0x7169D38820dfd117C3FA1f22a697dBA58d90BA06",
+      "network_id": 97
     },
     "price_per_base_duration": "100",
     "credited_amount": "100000",
@@ -17,8 +17,8 @@
   {
     "subscription_type": "Developer",
     "token_params": {
-      "token_address": "0xa8d3dee6671c4fdac4743a1eb1F276EabD4ba302",
-      "network_id": 56
+      "token_address": "0x7169D38820dfd117C3FA1f22a697dBA58d90BA06",
+      "network_id": 97
     },
     "price_per_base_duration": "200",
     "credited_amount": "200000",
```

### Increasing Account's Credits 

TODO

