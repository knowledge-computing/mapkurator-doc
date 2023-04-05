High-resolution historical map images typically contain a large amount of detail, which can result in very **large file sizes**. This can pose a challenge when working with the images, due to the large **memory** required.

To overcome this challenge, we crop the map images into smaller tiles, where each tile contains only a portion of the overall image. In our case, the tiles are `1000x1000` pixels in size.

Processing the tiles with text spotting model in parallel means that multiple tiles are processed simultaneously, which can significantly reduce the amount of time it takes to work with the images. For example, with `batch_size=24`, the spotting model can detect and recognizes the text in `24` map tiles in the same time. 

<img width="880" alt="image" src="https://user-images.githubusercontent.com/5383572/230233508-6d552698-b50d-4218-8f45-c437687a552d.png">

