---
title: "Snap-deals"
description: "A one-message protocol for updating any sector with new data without re-sealing. This allows users to utilize the confirmed storage available in the network, while also allowing storage providers to earn storage rewards without having to seal new sectors."
lead: "A one-message protocol for updating any sector with new data without re-sealing. This allows users to utilize the confirmed storage available in the network, while also allowing storage providers to earn storage rewards without having to seal new sectors."
draft: false
menu:
    docs:
        parent: "storage-providers"
weight: 492
toc: true
---

When clients want to store something using Filecoin, they must first find a storage provider willing to accept a deal. Once the storage provider and client have agreed upon the terms of the deal, the client starts to transfer their data to the storage provider. Once the transfer is complete, the storage provider seals the data, and the Filecoin blockchain verifies that the data is stored correctly for the length of the storage deal. 

Storage providers earn rewards in two ways:

1. Committing storage space to the network. 
1. Charging clients fees for storing data. 

Most of the storage available on the Filecoin network, also known as _committed capacity_, is storing _dummy data_. If there aren't any users that want to store something at the time that the sector is committed, then the storage provider fills in the binary space with lots of `0`s. This means that a large portion of the storage available on the Filecoin network isn't being used for anything particularly important.

{{< alert icon="tip" >}}
If you'd like to see an in-depth explanation of how Snap-deals work, take a look at the [Filecoin Improvement Proposal FIP-0019](https://github.com/filecoin-project/FIPs/blob/master/FIPS/fip-0019.md).
{{< /alert >}}

## Simplified explanation

Snap-deals allow storage providers to accept deals from users and place that user's data into a block of storage that had already been committed. That was a bit of a mouthful, so picture it like this.

Imagine there is a town with a very long shelf. Anyone in this town can store anything they want on this shelf. When a townsperson wants to store something, they give that _thing_ to a storage provider. The storage provider builds a wooden box, puts the townsperson's stuff into the box, and then puts the box on the shelf.

![A shelf representing the Filecoin network.](shelf.png)

Some of the boxes have useful stuff in them, like photographs, music, or videos. But sometimes, the storage providers don't have any townspeople lining up to put useful stuff into the boxes. So instead, they put packing peanuts in the box and put that on the shelf. This means that there are a lot of boxes being made to just hold packing peanuts. Making boxes takes a long time and takes a lot of work from the storage provider.

![Types of data in a Filecoin sector.](data-types.png)

Instead of creating a new box every time someone wants to store something, it'd be better if we could just replace the packing peanuts with useful stuff! Since nobody cares about the packing peanuts, nobody is going to be unhappy with throwing them out. And the storage provider gets to put useful stuff on the shelf without having to create a new box! Things are better for the townsperson, too, since they don't have to wait for the storage provider to create a new box!

![Emptying sectors of dummy data to fill them with real data.](emptying-boxes.png)

This is a simplified view of how Snap-deals work. Instead of a storage provider creating an entirely new sector to store a client's data, they can put the client's data into a committed capacity sector. The data becomes available faster, things are less expensive for the storage provider, and more of the network's storage capacity gets utilized!

## Benefits

Snap-deals benefit all users throughout the Filecoin ecosystem. Storage providers are able to use their storage capacity more effectively and speed up the deal-making process. Snap-deals also make the data from clients available much faster.

## Performance information

Storage providers from the Lotus [community tested Snap-deals performance](https://github.com/filecoin-project/lotus/discussions/8127) with the following hardware and results:

| Provider<br>Hardware | UpdateReplica<br>(RU) | ProveReplicaUpdate<br>(PR2) | ProveCommit<br>(C2) |	
| --- | --- | --- | --- |
| **CPU**: 3975WX<br>**GPU**: 2x RTX 3090 (CUDA) <br>**RAM**: 512 GB<br>**SWAP**: 0 GB<br>**Sector**: 32 GiB | 5m 38s | 7m 52s | 6m 57s |
| **CPU**: EPYC 7F72<br>**GPU**: 2x RTX 2080ti (CUDA) <br>**RAM**: 256 GB<br>**SWAP**: 20 GB<br>**Sector**: 64 GiB | 9m 19s | 19m 0s | 16m 10s |
| **CPU**: EPYC 7502<br>**GPU**: RTX 3080 (CUDA) <br>**RAM**: 512 GB<br>**SWAP**: 0 GB<br>**Sector**: 64 GiB | 12m 59s | 23m 13s | 18m 24s |

<!-- 

## Test snap-deals

If you are a storage provider and want to get to grips with Snap-deals, then follow this quick guide! You will learn how to set up a local Filecoin network, create some basic deals, and then convert those deals to Snap-deals.

### Start a Lotus local-net

### Create basic deals

### Convert deals to Snap-deals

## Video example

Here is a simple run-through of how Snap-deals work:

-->