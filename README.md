# Global-Wheat-Detection
Showcases the use of deep learning to detect wheat heads from crops. The project is based on this Kaggle Competition: https://www.kaggle.com/c/global-wheat-detection.

**Here's a description of the prediction task**:

In this competition, you’ll detect wheat heads from outdoor images of wheat plants, including wheat datasets from around the globe. Using worldwide data, you will focus on a generalized solution to estimate the number and size of wheat heads. To better gauge the performance for unseen genotypes, environments, and observational conditions, the training dataset covers multiple regions. You will use more than 3,000 images from Europe (France, UK, Switzerland) and North America (Canada). The test data includes about 1,000 images from Australia, Japan, and China.

[- Source](https://www.kaggle.com/c/global-wheat-detection)

## Data
An overview is available here: https://www.kaggle.com/c/global-wheat-detection/data. 

The dataset includes images that either have wheat heads or do not have them. Here are some examples:

![](https://i.ibb.co/s6c7bNk/download.png)

![](https://www.kaggleusercontent.com/kf/33370350/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..pixyW0L3pAEJIzCb6oUHAw.efaeYtu1SYMdVYd9usvfOBc-Js8vOK84jN5nuBQ5waTcTPCnoeMuOMkU8AfFY43Pc9OX1bfgcGdC2OLBYyzh46Mny5iYy4R3ImY8nB-acnqRUMu_Wo5KRnw2MpxW6yIU4Nx-xC2Y4J79WUsLE2AAS0OjTQ7zwkybQQF65As_l7IhZGH8Kp4CSQ6DKC3ULI2x7cPkdOo4kNThmq4DuXVI2-Ugby7HcT-Oq9vD1tIm1phlmed1A0pqp9xSdN3GjZGVrIJHbGHbx072C580Ck_fAtN7BFaL3msEHOI2337QIKxPY-EeNKOjFehoegGiA_AbLSVd_UDIS6Gzb7S-czC_zTeK3WUg8oL3cx8Is0KzAUGyjwSs1w3_qwI65LAVnTJEIti1FQ9qRajbQC_hS98Br-SyUk4NwavNGyeWlNJftGBZ-q0YrzfMSUQarTNXZKk0HdJ1ubDD2JOB1RKVaqfCvBfOw8im6rMBxFuIBd1LV7Y-lF5slJgC8BqfyUhcTTFBhL8TBgH1LnW0-Xh6VW5X6GhvJNXYEmeXziGcTwz3AVPKVnbzZNpj-big0TnQjNWnPqncgEc8RyaXUc-_8vzqmdYAREFWB6bBUheSKVJdo5QJbFnKDrTaOwYiyO-d8NVNeKgDba8JRureN-B_Ks13S5jBFKkelyaPqAb9jkUW8icmQfuFfdK7C5YQtALOay43.ht0xqC0KZ0Y2d9ZD-GWbQw/__results___files/__results___35_0.png)

I used the following command to obtain the data:
```
$ kaggle competitions download -c global-wheat-detection
```

This is an object detection task and the project uses [TensorFlow Object Detection (TFOD) API ](https://github.com/tensorflow/models/tree/master/research/object_detection).

## About the files
- `Basic_EDA.ipynb`: Performs basic data visualization on the provided dataset. 
- `Data_Prep.ipynb`: Prepares the data in a TFOD API compatible format. 

## Results

## Acknowledgement
- ML-GDE program for granting me GCP credits.
- TensorFlow Research Cloud for granting me Cloud TPU credits. 

The project extensively uses GCP's AI offerings such as AI Platform. Specifically, I used AI Platform Notebooks and AI Platform Jobs. For storage I used GCS buckets. 
