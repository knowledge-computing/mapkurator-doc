High-resolution historical map images typically contain a large amount of detail, which can result in very large file sizes. This can pose a challenge when working with the images, due to the large memory size required.

To overcome this challenge, we crop the map images into smaller tiles, where each tile contains only a portion of the overall image. In our case, the tiles are 1000x1000 pixels in size.

Processing the tiles with text spotting model in parallel means that multiple tiles are processed simultaneously, which can significantly reduce the amount of time it takes to work with the images. For example, if you have a large number of tiles to process, you can split the workload across multiple processors or computers, with each one working on a subset of the tiles.

