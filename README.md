# Udagram Image Filtering Microservice

This API makes use of nodejs to read an image from an URL and then passes it to python with a sub process. Python then filters the image, finds the edges with OpenCV and returns an absolute path to the image to Nodejs.

The processed image, will then be sent as response to the user. Once the image is received by the user, all the temporary working files, will be deleted from the server.


### Setup Node environment

In order to use this service, it is necessary to have Nodejs v10.16 (or grater) installed on the machine.

Open a new terminal within the project directory and run:

1. Initialize a new project: `npm i`
2. run the development server with `npm run dev`

## Available endpoints

This micro service has two endpoints:
1. '/'
2. '/filteredimage

The first endpoint sends a short message to the user with some tips on how to use the service.

The second endpoint is the important one. It accepts the following query parameters:

```
image_url [required]
lower [optional - upper parameter must be provided]
upper [optional - lower parameter must be provided]
```

The first parameter, `image_url`, is mandatory, and is a full URI that points to an image.
We'll make use of the Jimp library to check whether the url points to a valid image or not.

`lower` and `upper` are optional parameters and must be used jointly. These two parameters specify the lower and upper threshold limits for the OpenCV Canny function used to find the image edges.

If lower and upper are not specified, python will use a method to auto detect the best thresholds.

### Endpoint examples

Endpoint example without thresholds:
```
http://localhost:8082/filteredimage?image_url=https://images.unsplash.com/photo-1529940340007-8ef64abc360a?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=753&q=80
```

Endpoint example with thresholds:
```
http://localhost:8082/filteredimage?image_url=https://images.unsplash.com/photo-1529940340007-8ef64abc360a?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=753&q=80&lower=50&upper=200
```

## Deploying your system

The deploy to elasticbeanstalk run the following command in the root of your project:
```sh
$ eb init
```

To create the environment in aws with:
```sh
$ eb create
```
