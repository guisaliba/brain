---
title: How does a Vision-Language-Model (VLM) work? - Groundlight AI
source: https://www.groundlight.ai/blog/how-vlm-works-tokens
author: Leo Dirac, Sunil Kumar, Francine W
published: 2024-07-16
created: 2026-06-08
description: How do LLMs like ChatGPT understand images? We go through how the neural networks inside a VLM communicate with each other.
tags:
  - clippings
---
## How does a Vision-Language-Model (VLM) work?

How do LLMs like ChatGPT understand images? We go through how the neural networks inside a VLM communicate with each other.
## Background: Gen-AI, LLMs, and Computer Vision

Gen-AI's ability to author text and create images has captured the world's imagination, and catapulted the previously academic discipline of Machine Learning into Artificial Intelligence. But still most commercially useful applications of these techniques are for automatic decision making - so-called "discriminative" tasks, where inputs are analyzed to pick from a relatively small number of outputs, like "Is this order ready?" The dominant architecture of Gen-AI is the Large Language Model (LLM), a transformer neural network which takes arbitrary prompt input text and produces output text.

![](https://cdn.prod.website-files.com/664b7cc2ac49aeb2da6ef127/6835ee799cd4248a2fb9fa96_How%20does%20a%20VLM%20work_LLM%20input%20text%20and%20output%20text.jpg)

In the visual domain, commercial and industrial systems have long relied on computer vision or machine vision for decades for applications like quality control, security, and safety systems. All of these applications require "visual understanding" - which is to say, looking at a picture, analyzing it, and making discrete judgements about it to inform decisions. The recent breakthroughs in Gen-AI have been surprisingly slow to improve visual understanding. The combination of visual understanding with LLMs is generally referred to as a Visual-Language Model (VLM), which is an LLM that can take images as input. This allows the VLM to use the images as part of their prompt for whatever generative task such as writing a poem about the image (easy), or more usefully, answering specific questions about it (difficult).

## How do Vision-Language Models (VLMs) work

At a high-level, VLMs combine an LLM with another model that processes images. There have been many variations proposed for how to do this, but nowadays a standard pattern has emerged which is fairly straightforward, depicted below. It combines an LLM which is pre-trained only on language, with a ViT which is pre-trained only in images, and then the two are re-trained to work together.

![](https://cdn.prod.website-files.com/664b7cc2ac49aeb2da6ef127/6835ef5d84eb2d5a965a9f0e_How%20does%20a%20VLM%20work_Image%20to%20ViT%20to%20LLM.jpg)

### Tokens, Embeddings, and Vectors, oh my!

In order to understand how VLMs handle images, first let's peel back a layer of the onion on how LLMs work. Being neural networks, everything they do is based on high-dimensional vectors. So before it can process text, an LLM must first convert the text into a sequence of vectors, which are also referred to as tokens.

This is done with two components, the first of which is the "Tokenizer". The tokenizer splits the input prompt into a series of so-called "word pieces", which might be whole words, or partial words, or even just individual characters. Each LLM has its own tokenizer, but the commonly-used LLaMA tokenizer breaks the word "Robotics" into three tokens: \[Rob\] \[ot\] \[ics\], but as luck would have it, the lower-case word "robotics" can be represented with just two tokens: \[robot\] \[ics\]. Token boundaries are fairly arbitrary - feel free to play with them yourself [here](https://belladoreai.github.io/llama-tokenizer-js/example-demo/build/).

Next, each word-piece is converted into a vector through an embedding layer. This is literally just a big lookup table that translates any of the ~32,000 word-pieces into a unique [semantically-meaningful](https://arxiv.org/abs/1301.3781) vector. Here, we're calling these vectors language tokens or "lang tokens". The LLM processes these language tokens, applying its layers of attention and feed-forward networks to predict the next token after each provided, and thus recursively generating a set of output tokens, which start as language tokens in the vector space.

![](https://cdn.prod.website-files.com/664b7cc2ac49aeb2da6ef127/6835ef967b0ca4847f4ebe50_How%20does%20a%20VLM%20work_Wordpieces_Lang%20tokens.jpg)

### Converting vectors back into text

How these output vectors/tokens get converted back into text is particularly import for what we're going to do later, so we'll go into some detail on it, and even bring in some math.

To convert a lang token into a word-piece, we use another embedding layer, which is effectively (or sometimes literally) just the transpose of the input's Embedding matrix. Here, the model performs what's essentially a reverse lookup in the embedding space. It compares each output lang-token vector to all the vectors in its embedding matrix, finding the closest match. This might sound complicated like you'd need a vector database for it, but actually very simple, requiring a simple matrix multiplication, and is exactly what happens in any SoftMax classification output layer, such as the final stage of an LLM. (Readers who like linear algebra are invited to prove to themselves this nugget of wisdom: ***Maximizing the dot-product between vectors is the same as minimizing the cosine-distance, if all the vectors are unit-length.***) The word-piece corresponding to the most similar embedding vector is then selected as the output word-piece.

Finally, a de-tokenizer, which does little more than concatenate these word-pieces together, converts it all back into human-readable text.

### The ViT acts as an Image Tokenizer

To process an image as part of the input prompt, a VLM starts with a pre-trained Vision Transformer (ViT).

Images are first preprocessed into a set of image patches, often 14x14 pixel square (although of course other sizes are possible), and then these patches are each converted (linearly projected) into a vector space. So now we have a single high-dimensional vector for each 14x14 pixel patch of the input image, and we'll typically have hundreds of these image patch vectors.

The image patch vectors are then sent through a neural network that is pre-trained for image analysis - typically a ViT (Vision Transformer) like CLIP.

After the ViT's processing, these tokens are still in the vector space of the ViT, which has nothing to do with the word token space of the LLM. For CLIP, these vectors are 768-dimensional. But an LLM like Vicuna uses 4096-dimensional vectors. So the most important part of the VLM is the projection layer which converts the image patch vectors into the word token space of the LLM.

In so-called " [LLaVA](https://arxiv.org/abs/2304.08485) " style VLMs this projection layer is very simple (linear, or a small MLP), acting on each token individually - meaning the number of tokens going into the LLM is the same as the number of patches in the image. But some designs (like BLIP) use a more complex projection layer, which is actually its own Transformer module that outputs a smaller number of tokens than it took as an input - effectively learning a "summary" of the image. But the current trend in the research literature seems to be towards using simple projection layers, and putting the smarts in the LLM. Intuitively this makes sense, because LLMs are extremely powerful on a wide variety of tasks. Whereas training a complex projection layer would require a large amount of high-quality aligned image-text data, which is much harder to come by these days compared to the pure-text data used to train LLMs, or the purely visual data used to train the image modules.

### Putting it all together: The full VLM Architecture

Now we can appreciate the beauty of a fully-armed and operational VLM. We have what you might call a "vision-tower" which takes the image and converts it into lang tokens to send into the LLM. And a much simpler "text tower" which is a staple part of standard LLMs.

Okay, that's all well and good. But frankly, you can get this background in lots of places and papers. But at Groundlight, we're not satisfied with the status quo. And sadly, the status quo of public VLMs is still super not good ([recent paper](https://www.arxiv.org/abs/2407.06581)). So to investigate, we asked ourselves what's *really* going on in there? What is happening in that projection layer? What are those lang tokens actually saying about the image?

## What is the VLM saying about your image?

So how do we interpret the tokenized description of the image before it goes into the LLM? To put it another way, **"what are all those image tokens saying in words?"** Because the vision tower is outputting lang tokens in the same embedding space as text, we can try to interpret these tokens as text. But it's not as simple as you might expect, because the vector embeddings have a TON more information than the text tokens. From a data/memory/CS perspective, this is clear: 1024 \* 32-bit floats contain 4kB of data, compared to 4 bytes of data in an integer representing a text token. Of course, the LLM's output layer does exactly this conversion - from vector back to wordpiece. But there the LLM is "trying" to output a single chunk of text. But the ViT is deliberately using the extra data to encode more information. E.g. a single image patch of part of a furry black dog tail might properly be encoded as the weighted vector of lots of wordpieces like 1.79\*dog + 1.21\*cute + 1.11\*fur + 0.71\*black + 0.32\*gray + 0.22\*tail.

What we did here is for each lang token coming out of the projection layer, to look back in the tokenizer's Embedding matrix to find its nearest neighbors. This is a vector search operation, here using Euclidean (L2) vector distance. When we've found the closest vectors, we convert these back into token ids, and word-pieces from the LLM's vocabulary. By placing these word-pieces directly on the image in the appropriate location, we can visualize what the vision tower "sees" in each patch, and thus what the VLM is being told about the image.

However, the floating-point vectors contain far more information than the word-piece. If you think about "bits of information" in each representation, there are ~32,000 word-pieces, which is very close to 2^15, so the choice of which word token requires 15 bits of information. But each floating point number in the vector uses 16 bits of storage - although it's debatable how much of that precision is useful. The most extreme neural-network compression gets down to 4 bits of precision, so let's say each dimension is worth 4 bits of information. Then the 4096-dimensional vector represents ***16 kilobits*** of information - way more than the 15 bits from the word-piece.

When the LLM is fine-tuned to be a VLM, it learns to understand these subtleties - the lang tokens from the vision tower are saying more than just one word-piece. To further visualize this, we find the 8 nearest vectors. If you hover over a token, you will see all 8, sorted by the strength of association. For example in the patches under the boardwalk you see that the lang tokens include a combination of \[road\] and \[gray\] indicating that both of these concepts are present and being fed into the LLM.