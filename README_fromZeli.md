0.0. Fork (and star) my repo, and then clone the forked to your local.
0.1 If you miss some package when running the code, just install it in a regular way(pip or conda)
1. run the save_model_weights.py
2. download the dataset from https://www.image-net.org/challenges/LSVRC/index.php,ImageNet,Large Scale Visual Recognition Challenge 2012 (ILSVRC2012) (validation dataset, 6.3GB)
2.1 unzip and run the valprep.sh to the downloaded file.
3. Create a folder called 'result' in your project
4. make sure your project looks like:

project:
    evaluation.py
    runtime.py
    ViT-B_16-224.npz
    ILSVRC2012_img_val:
        n0......:
            (lots of).JPEG
        n0......
        (lots of)
        n0.......
    pipeedge:
        others
        quantization:
            basic_op.py
            others
    result

5. you dont need to modify any in the code

This is the example(quant at the 22th layer using 8 bit).Please wait at the beginning of the running, since the program will prepossess the dataset and the model, after a while, you will see the result line by line.

```sh
python evaluation.py -pt 1,22,23,48 -q 8,8
```

This version is the default bit allocation:
e=int(bit/2) and m=bit-e-1

If you need to change the bit allocation, you could simply modify the 7th line in pipeedge/quantization/basic_op.py, then it will change the bit allocation.

For example, from e=int(bit/2) to e=2.

This version of code will automatically clamp the data at first. If no, please take a look at 83th of runtime.py

If you run this code on discovery, you may use the 179th line in evalution.py instead of downloaded the dataset to discovery. 
