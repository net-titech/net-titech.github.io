---
layout: post
title: Deep compression case study
excerpt: "Reverse engineering Song Hans' compressed AlexNet"
categories: [Tutorials]
comments: true
---

In this post, we study the result of Song Hans' work on AlexNet. Since the
encrypting code is not provided, we analyze the decompression code provided
on the author's
[github repository](https://github.com/songhan/Deep-Compression-AlexNet) to
have a clear understanding of the compression scheme. There are two main
techniques contribute to the small size of the compressed AlexNet:
1. Values clustering - Instead of having different values for each weight
matrix, each layer is limited to have only 256 distinct values (convolutional)
or distinct 16 values (fully connected). These values is encoded using 8-bit
integer and 4-bit integer respectively.
2. Running sum encoding for the indexing array - Each weight is stored as a
sparse array (only non-zero elements are stored). To avoid large indexing
values (up to several millions), the index array is stored by the difference of
the non-zero index and the array index only. (This scheme enables Huffman Coding
to be effective later).

## Binary file layout

The provided binary file `AlexNet_compressed.net` is organized into a header
containing the number of non-zero elements in each layers `nz_num` and a body
containing data for each layer. Each layer has 4 main parts: `codebook`
contains the distinct float values of the layer, `bias` contains the bias
values (no compressing for bias), `spm_stream` contains the integer encoding
for each non-zero elements in the weight matrix, and `ind_stream` contains the
index for each non-zero elements.

![Binary file](https://net-titech.github.io/img/deep-compression-hans-compressed-file.svg)

In the figure above, each part name is given corresponding to the naming in
the provided `decode.py` file. Below the name is the size of the array (we will
provide details in the following sections). Yellow stands for `unsigned integer`
data type, blue stands for `float` data type.

## Header

The file header contains 8 32-bit unsigned integers representing the number of
non-zero elements in each layer. There are 8 layers in AlexNet. In the
decompression code, this array is named `nz_num`.

```python
layers = ['conv1', 'conv2', 'conv3', 'conv4', 'conv5', 'fc6', 'fc7', 'fc8']
# Get 8 uint32 values from fin (AlexNet_compressed)
nz_num = np.fromfile(fin, dtype = np.uint32, count = len(layers))
nz_num = array([29388, 118492, 309138, 247913, 163904, 4665474, 1959380,
                1061645], dtype=uint32)
```

## Compressed data for each layer

There are two types of layers in AlexNet namely convolutional and fully
connected. As we mentioned above, each convolutional layer has 256 distinct
values, while each fully connected has 16 distinct values. These distinct values
are stored in `codebook` section as 32-bit floats. The encoding is stored as
8-bit or 4-bit unsigned integers. We take the first convolutional layer `conv1`
as an example.

Since `conv1` is a convolutional layer, each elements in the weight matrix is
encoded using 8-bit. The `codebook` has size 256.

```python
# Read codebook from file, codebook_size=256 in this case
codebook = np.fromfile(fin, dtype = np.float32, count = codebook_size)
```

Bias for each convolution is read and copy to the network. In this case, there
are 96 32-bit floats biases corresponding to 96 convolutional kernels. No
compression is provided for biases.

```python
bias = np.fromfile(fin, dtype = np.float32, count = net.params[layer][1].data.size)
np.copyto(net.params[layer][1].data, bias)
```
