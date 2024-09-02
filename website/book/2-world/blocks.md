# Blocks

## Intro

Before diving into how to deal with blocks, we need to know how Valence stores and manages everything.

#### LayerBundle

A `LayerBundle` is just a Bevy bundle that creates a `ChunkLayer` and `EntityLayer` (In the `chunk` and `entity` fields respectively).

#### ChunkLayer

A `ChunkLayer` is a component that contains the chunks and dimension information of a Minecraft world. You need to set a player's `VisibleChunkLayer` to your `ChunkLayer`'s Bevy Entity ID in order for the player to see it.

#### BlockState

A `BlockState` is used to represent a type of Minecraft block. For example, a grass block is `BlockState::GRASS_BLOCK`. A `BlockState` can be converted into a `Block` struct, so for many functions you only need to pass the relevant `BlockState` when creating a block without extra data.

#### Block

A `Block` struct contains all the relevant information about a certain block (it's `BlockState` and NBT data).

#### BlockRef

A struct that acts as an immutable reference to a `Block`.

## Creating blocks

We've already seen how to create blocks in the [setup chapter](../1-getting-started/setup.md) - the `.set_block()` function of `ChunkLayer`. Let's review by looking at this code snippet:

```rust
chunk_layer.set_block([0, 64, 0], BlockState::GRASS_BLOCK);
```

This code sets a grass block at the coordinate `0 64 0`.

## Removing a block

To remove a block, just replace it with an air block.

```rust
chunk_layer.set_block([0, 64, 0], BlockState::AIR);
```

## Checking the block at a coordinate

To get the block at a certain coordinate, use the `.block()` function of `ChunkLayer`. It will return a `BlockRef` of the block at that position.

```rust
let block = chunk_layer.block([0, 64, 0]);
println!("Block at [0, 64, 0]: {:?}", block);
```