For now, follow operator framework - https://operatorframework.io/

Also check https://sdk.operatorframework.io/

and https://olm.operatorframework.io/

Features
- Install a particular version of Redis standalone
- Install a particular version of Redis HA with sentinel
- Install a particular version of Redis cluster with primary and replica shards
- Upgrade to a particular version of Redis standalone
- Upgrade to a particular version of Redis HA with sentinel
- Upgrade to a particular version of Redis cluster with primary and replica shards
- Support operations on Redis cluster like - add primary shard, add replica shard, remove primary shard, remove replica shard

I need to check more about the operations on a Redis Cluster, and also about operations on Redis standalone and Redis HA

Also, I need to check about disaster recovery stuff like - backup, restore etc

And I need to support Redis with persistence and without persistence too, hmm

Upgrade strategy would kind of be like - replicate from existing and then bring down old / existing thing. For example, upgrade in Redis standalone - introduce another newer version Redis standalone, which replicates from existing Redis and then finally do the switch over / failover. Something to think about is - how to handle the client connections - how to cut it off during failover. Finally get rid of the old Redis

What about support for downgrades? Hmm, something to think about

For Redis cluster upgrade strategy - simply add new primary and replica shards with new Redis version I guess? And allocate (and move) hashslots to the new primary shards? And slowly start moving all the hashslots to the new primary shards? And then get rid of the old version primary and replica shards I guess? I can't think of a better idea as of now. And this makes a lot of sense in terms of a rolling deployment. Immediately switching over to a new thing doesn't seem possible and doesn't seem to make sense. A smoooth and seamless switchover is key I think


