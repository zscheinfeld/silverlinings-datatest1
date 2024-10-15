# Instructions for testing this surrogate model

## Necessary files

The `tensorflowjs` files necessary for running the surrogate model are in the `WebSurrogate/tf_model`.  These include a JSON file containing the model structure and metadata and at least one binary file with the model weights.

These files are created with the `TrainSurrogate.ipynb` notebook in the `WebSurrogate` directory.  This notebook relies on one file, `ExampleData.csv`, which is also in the `WebSurrogate` directory. For now, this file is just some data created outside of model runs of the macroeconomic model.  In the future, we will use actual model runs to create these data.

## Start a local server

One can do this with Docker.  To start a server with the files in this directory, run the following command in the terminal (updating the path to the location of the `WebSurrogate` directory on your machine):

```
docker run -d -p 8080:80 -v /Users/jason.debacker/repos/WebSurrogate:/usr/share/nginx/html/ --name my-nginx-server nginx
```

## Navigate to the test page

Go to `http://localhost:8080/js_viz_test.html` in your web browser.  This is simple webapage that takes one input and, after clicking the "calculator" button, will return the output of the surrogate model given a prediction based on the input.

## Making changes

The script to edit the webpage is the `js_viz_test.html` file.  This file is a simple HTML file that loads the necessary libraries and the TensorFlow.js model.  It then uses the model to get a prediction from the surrogate model given an input.

# Notes on training the surrogate model

If you'd like to train the model and convert the new output to the tensorflowjs format, you can do so by running the `TrainSurrogate.ipynb` notebook in the `WebSurrogate` directory.  This notebook will train the model and save the model weights and structure and then convert them to tensorflowjs format and save those in the `tf_model` directory.

For this notebook to run successfully, you will likely need to create the `ws-env` virtual environment using the `environment.yml` file in the `WebSurrogate` directory.  You can do this by running the following commands in the terminal:

```
conda env create
conda activate ws-env
```

You can then execute the `TrainSurrogate.ipynb` notebook, selecting the `ws-env` kernel.
