# MongoDB Utilities

ShardConfigSync
---------------
Sync shard metadata, copies sharding metadata from one cluster to another.

```
java -cp mongo-util.jar com.mongodb.shardsync.ShardConfigSyncApp \
    -s mongodb://admin:mypassword@source:27017/?authSource=admin \
    -d mongodb://destination1:27017 \
    -f db1 -f db2 \
    -m sh_0|shard_A -m sh_1|shard_A -m sh_2|shard_B -m sh_3|shard_B \
    -p /Users/mh/go/src/github.com/10gen/mongomirror/build/mongomirror \
    -dropDestinationCollectionsIfExisting \
    -syncMetadata
```

Run mongomirror process for each shard

```
java -cp mongo-util.jar com.mongodb.shardsync.ShardConfigSyncApp \
    -s mongodb://admin:mypassword@source:27017/?authSource=admin \
    -d mongodb://destination1:27017 \
    -f db1 -f db2 \
    -m sh_0|shard_A -m sh_1|shard_A -m sh_2|shard_B -m sh_3|shard_B \
    -p /Users/mh/go/src/github.com/10gen/mongomirror/build/mongomirror \
    -dropDestinationCollectionsIfExisting \
    -mongomirror
```

MongoReplayFilter
-----------------
This tool will filter the operations captured to only the essential operations, e.g. internal ops are removed and replies are removed from the resulting BSON.

This will also transcode 2010 opcodes to 2004 opcodes, which is useful when capturing sharded operations between a mongos and a mongod. Additionally, mongoreplay currently does not properly handle $query commands which will be sent in certain cases, e.g. when a non-default ReadPreference is specified.

Also supports limiting the number of operations (-l) and filtering fields from updates.

Download:
```
wget -O mongo-util.jar https://github.com/mhelmstetter/mongo-util/blob/master/bin/mongo-util.jar?raw=true
```

Run:
```
java -cp mongo-util.jar com.mongodb.mongoreplay.MongoReplayFilter -f record041020185.bson
```
The output file will be written with the same name + `.FILTERED`.

MongoReplay
-----------
Similar to the mongoreplay utility, this encorporates some of the "hacks" implemented by MongoReplayFilter, and directly play the traffic to the desitination cluster. This tool will filter the operations captured to only the essential operations, e.g. internal ops are removed and replies are removed from the resulting BSON.

This will also transcode 2010 opcodes to 2004 opcodes, which is useful when capturing sharded operations between a mongos and a mongod. Additionally, mongoreplay currently does not properly handle $query commands which will be sent in certain cases, e.g. when a non-default ReadPreference is specified.



Download:
```
wget -O mongo-util.jar https://github.com/mhelmstetter/mongo-util/blob/master/bin/mongo-util.jar?raw=true
```

Run:
```
java -cp mongo-util.jar com.mongodb.mongoreplay.MongoReplayFilter -f record041020185.bson
```
The output file will be written with the same name + `.FILTERED`.


DiffUtil
-----------------
Download:
```
wget -O mongo-util.jar https://github.com/mhelmstetter/mongo-util/blob/master/bin/mongo-util.jar?raw=true
```

Run:
```
java -cp mongo-util.jar com.mongodb.diffutil.DiffUtilApp
```
