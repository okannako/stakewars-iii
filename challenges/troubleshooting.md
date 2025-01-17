# Troubleshooting guide for Stake Wars III
* Published on: 2022-07-25
* Updated on: 2022-07-25
* 
This guide is made to solve the most common questions related to a node not working as expected. Feel free to make your own contributions or suggestions on what this guide should include.

## My node is not producing chunks/blocks
Not producing means:

```
"num_expected_blocks": XXX,
"num_expected_chunks": XXX, 
"num_produced_blocks": 0,
"num_produced_chunks": 0,
```

Try this 2:

```
near view <POOL_ID> get_staking_key '{}'

cat ~/.near/validator_key.json | grep public_key
```
🗒️  ** Both keys must match **. If they DO NOT update the staking pool key ❗ 

Update staking pool key:
```
near call <POOL_ID> update_staking_key '{"stake_public_key": "<PUBLIC_KEY>"}' --accountId <ACCOUNT_ID>
```

If match:
Check validator_key.json

```
cat ~/.near/shardnet/validator_key.json
```

account_id must be like : xx.factory.shardnet.near
If not update it, save and stop/start neard

## Explorer is not showing my transactions/not updating
In case that explorer.shardnet.near.org is not working, review the RPC status on the corner. 

OK (Green indicator)
![img](./images/rpc-status.png)

RPC not available (Yellow indicator)
![img](./images/rpc-status-down.png)


If it is in other color than green it should be passing unstable behavior. Wait until in stabilize.

In case you can user near CLI to review validators information.

```
near proposals
near validators current
near validators next

```

## I cannot run neard, it shows ‘Failed to open the database’
This is common because there is a current service using the files. Probably another neard service.

Try running the top command and verify there is no neard service already running.


My staking pool lost the tokens I delegate to it
In case you delegated tokens to your staking pools before one the hard forks made to the shardnet network, your account could be deleted by the fork.

Just create a new account and delegate enough tokens.

```
near call <staking_pool_id> deposit_and_stake --amount <amount> --accountId <accountId> --gas=300000000000000

```

## ***Common Node Errors and Solutions*** by Open Shards Alliance
In case none of the above worked, you can use this guide. In this document you will find a general rules on how to solve problems related to a node validator running on NEAR Protocol. 

* [Common Node Errors and Solutions](https://near-nodes.io/troubleshooting/common-errors) Guide by OSA.

## Ask community

[Join official NEAR Discord server](https://discord.gg/V3Z6CsEJ7Y), where you fill find the #stakewars channel for solving questions.This is a community fueled channel, feel free to contribute.


