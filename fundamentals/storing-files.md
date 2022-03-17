# Storing files (blobs)

In addition to serving JSON state, Redwood nodes can find, fetch, and serve files, much like a BitTorrent client or an IPFS node. In fact, thanks to the magic of [NelSON transclusion](state/nelson-linked-json.md), you can actually think of these files as _part of the state_.

Like with IPFS and BitTorrent, files are "content-addressed," i.e., they are identified and referred to by the SHA3 hash of their contents.

When your node becomes aware of a file that has been transcluded into a state tree, it queries the peer-to-peer network until it finds peers that can serve that file.

{% hint style="info" %}
Redwood's name for files is "blobs".
{% endhint %}

## Files as state

Let's imagine that our node subscribes to a state tree containing the following piece of state:

```json
{
    // ...
    "some-file.txt": {
        "Content-Type":   "link",
        "value":          "blob:sha3:ad1c881655b9590807af2ae0282f3e6253557b0f3a29faf4318c1dd6c2521596"
    },
    // ...
}

```

You might recognize this as a NelSON link. The `value` key, in this case, contains a reference to the file (by its SHA3 hash), rather than a link to other JSON state.

When the node becomes aware of this link, it will attempt to fetch the file from its peers. Once the file is downloaded, the node verifies the hash of its contents, and thereafter is able to serve it to others.

By transcluding the file into the state tree, we give users a more human-friendly way of accessing it. For example, in the case of the state tree above, if you were to navigate to [http://localhost:8080/some-file.txt](http://localhost:8080/some-file.txt), the node would serve you the file `ad1c881655b9590807af2ae0282f3e6253557b0f3a29faf4318c1dd6c2521596`.

## Content-defined chunking

Instead of treating a blob as a singular stream of bytes, Redwood stores files in "chunks." There are two reasons for this:

1. Downloads can be more easily parallelized (by default, the node will attempt to download 4 chunks from 4 different peers simultaneously, if possible).
2. Making a small change to a particular chunk in a file is much less likely to change the chunks before and after it, meaning that only a single, small chunk needs to be sent over the network and stored on disk.

To facilitate #2, Redwood uses a technique called "Rabin chunking" (or "Rabin-Karp chunking"), a form of content-defined chunking. As opposed to using a fixed chunk size, this technique is capable of finding the boundaries of the edit (in other words, the updated chunk) even without knowledge of the previous layout of the file.



**Recommended reading:**

{% embed url="https://en.wikipedia.org/wiki/Rabin%E2%80%93Karp_algorithm" %}

{% embed url="https://www.gluster.org/deduplication-part-1-rabin-karp-for-variable-chunking" %}

