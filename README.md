## Example: Predictive Analytics as a Service
This example deploys a neural network model for sales forecasting as a microservice accessible via an API `POST` request. The model was built using Keras/Tensorflow. The dataset is from [Kaggle](https://www.kaggle.com/c/rossmann-store-sales/download/train.csv.zip).

The framework was inspired by this [blog post](https://blog.pivotal.io/data-science-pivotal/case-studies/data-science-how-to-text-analytics-as-a-service).

The model is deployed using Jupyter Kernel Gateway 
* Jupyter Notebook (via the [Jupyter Kernel Gateway](https://github.com/jupyter/kernel_gateway))

The app is deployed on Cloud Foundry. This example deploys a trained model to forecast sales, but this framework can be modified for arbitrary predictive analytics and data science tasks.

### Model development

After cloning the repository first run the jupyter notebook in the model-development folder. This trains and exports the model into the model-deployment folder.

### Deploying to Cloud Foundry

If you do not have an account on a Cloud Foundry installation you can register for a free trial at [Pivotal Web Services (PWS)](http://run.pivotal.io). 

Download the Cloud Foundry Command Line Interface from the CF management console
or [the CF Github repo](https://github.com/cloudfoundry/cli).
This provides the `cf` command which you will use to interact with a CF installation.

Alternatively, you can install [PCF Dev](https://github.com/pivotal-cf/pcfdev) to install Cloud Foundry on a single work station.

### Deploying the model
#### Jupyter Notebook Microservice
```
cd model-deployment
cf push
```
### Using the neural network model via the API
The model accepts `POST` requests and returns a sales prediction for the given date. 
```
$ curl -H "Content-Type: application/json" -X POST -d '{"data":[ 0.,  1.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0., 1.,  0.,  1.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0., 0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0.,  0., 0.,  0.,  0.,  0.,  0.,  0.,  0.]}' neural-machines.cfapps.io/predict_timepoint
```
```
# returned result
{
  "Prediction": [1.33012]
}
```

An example of the app is currently deployed and be accessed at:

```
neural-machines.cfapps.io/predict_timepoint
```

### Resources

* [Sentiment classifier](https://github.com/crawles/gpdb_sentiment_analysis_twitter_model)
* [Python Cloud Foundry examples](https://github.com/ihuston/python-cf-examples)
* [Cloud Foundry Documentation](https://docs.cloudfoundry.org/)
* Pivotal Blog: [Model scoring as a service](https://blog.pivotal.io/data-science-pivotal/products/scoring-as-a-service-to-operationalize-algorithms-for-real-time)

### Issues to fix

Results are not scaled back yet using scaler.pkl.

### Author

`Balazs Feher`
