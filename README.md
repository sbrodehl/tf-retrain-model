# Retrain a Pretrained Model for New Categories

The full, detailed version of the tutorial(s) can be found on the tensorflow website
- [image retraining](https://www.tensorflow.org/tutorials/image_retraining)
- [image recognition](https://www.tensorflow.org/tutorials/image_recognition)

## Prerequeries

We will use the flower dataset to retrain the final layer of the inception model.
The dataset can be downloaded [here](http://download.tensorflow.org/example_images/flower_photos.tgz).
The images are already split up into folders, corresponding to the different classes.

This is for the lazy.
```bash
wget http://download.tensorflow.org/example_images/flower_photos.tgz
tar -xf flower_photos.tgz
```

The pretrained model will be downloaded once at the beginning of the training.

## Training

After preparing the data in the corresponding folders one can retrain the final layer of the model, also called transfer learning.
See `python3 retrain.py --help` for more information on training parameters (etc.).

```bash
python3 retrain.py --image_dir flower_photos
```

This will train for a fixed amount of steps. The progress can be seen in tensorboad.

```bash
tensorboard --logdir=/tmp/retrain_logs
```

Visit the [local tensorboard website](http://localhost:6006/) to see pretty things like accuracy or cross entropy.

## Inference

Once the retraining of the final layers is done one can use the model to do inference, that is, predict the class for unseen data.
Inference is run on a single image (`.png`/`.jpg`/`.bmp`/`.gif`).

```bash
python3 label_image.py --graph=/tmp/output_graph.pb --labels=/tmp/output_labels.txt --output_layer=final_result:0 --input_layer=Mul:0 --image=/FULL/PATH/TO/IMAGE.jpg
```

Using `flower_photos/daisy/100080576_f52e8ee070_n.jpg` the output will look like

```bash
daisy 0.938932
sunflowers 0.049032
dandelion 0.00581826
```
