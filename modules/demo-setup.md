1. Sign in to [Calico Cloud](https://www.calicocloud.io/home).
2. Make sure the selected cluster is `jlt-aks-genai`.

## Store Front Access
1. In Service Graph, go to the `pets` namespace.

2. Click on `store-front-*` to open the right-hand panel.

3. Click on `Top URLs`.

4. From the URL listed, pull out the IP address and paste this in a new tab in your browser.
   This will take you to the store front.

## Store Admin Access
1. In Service Graph, go to the `pets` namespace.

2. Click on `store-admin-*` to open the right-hand panel.

3. Click on `Top URLs`.

4. From the URL listed, pull out the IP address and paste this in a new tab in your browser.
   This will take you to the store admin page.

5. In store admin, select the products tab, then select Add Products.

   When the `ai-service` is running successfully, you should see the `Ask AI Assistant` button next to the description field.
   Fill in the name, price, and keywords, then generate a product description by selecting `Ask OpenAI` > `Save Product`.

   ![Generate product description](../assets/img/store-admin.gif)


## Pets RAG model

The pets-rag model is a python pod that web scrapes the store admin product info page, to load all pet products from the store into it's chat generation.
The 'R' of RAG is _retrieving_ the product info.
The 'G' of RAG is _generating_ answers based on the store information.

To use this, you will need:
* A paid OpenAI account and API key
* The IP address of the store admin


## Kubernetes
If you have a cluster, you can install the pets-rag pod by running:

``` bash
kubectl apply -f -<<EOF
apiVersion: v1
kind: Pod
metadata:
  name: pets-rag
  namespace: pets
  labels:
    app: RAG
spec:
  containers:
  - image: mapgirll/pets:pets-python-rag-amd64
    command: ["/bin/sleep"]  # Sleep command to keep the container running
    args: ["infinity"]  # Sleep indefinitely to prevent the container from exiting
    env:
    - name: OPENAI_API_KEY
      value: <API-KEY>
    - name: STORE-ADMIN-IP
      value: <IP-ADDRESS>
    imagePullPolicy: Always
    name: pets-rag
  restartPolicy: Always
EOF
```

This will deploy the pod in the pets namespace, which you may need to create first.

Once the pod is successfully running, you can run:

```bash
kubectl exec -it pets-rag -n pets -- python -i pets.py 
```

After a moment you will see the prompt `What questions do you have about the pet store?`.
Enter your question here, such as `What is the most fun toy you sell?`.

`What questions do you have about the pet store? What is the most fun toy you sell?`
`The most fun toy we sell is the "Ocean Explorer's Puzzle Ball." It challenges your pet's problem-solving skills with hidden compartments and treats, providing mental stimulation and entertainment.`

The pod will then exit, and to ask it another question you can re-run
```bash
kubectl exec -it pets-rag -n pets -- python -i pets.py 
```

## Docker

As long as there are no policies blocking access to the store-admin page, you can run the python pets-rag container using docker.

```bash
docker run -it -e "STORE-ADMIN-IP=<enter IP here>" -e "OPENAI_API_KEY=<paid API key here>" mapgirll/pets:pets-python-rag
```
As an example:
```bash
docker run -it -e "STORE-ADMIN-IP=4.246.54.60" -e "OPENAI_API_KEY=sk-MspeYY...aKWPok" mapgirll/pets:pets-python-rag
```
You will be prompted to ask a question, like this:

`What questions do you have about the pet store? Do you sell kibble?`
`I don't know.`
 or 

`What questions do you have about the pet store? Do you have any chew toys?`
`Yes, we have several chew toys available at the pet shop. Some options include the "Seafarer's Tug Rope" for $14.99, the "Nautical Knot Ball" for $7.99, and the "Contoso Claw's Crabby Cat Toy" for $3.99.`


## Calico Cloud

In Calico Cloud you will see the HTTP requests when you click on `store-admin-*` in Service Graph.

You can see that the `userAgent : Python-urllib/3.11`, which is the script that is scraping the admin page to retrieve product information.
The `srcNameAggr` is private, as docker is running locally.

```json
{
    "startTime": "6-25-2024 11:38:24 AM",
    "endTime": "6-25-2024 11:38:40 AM",
    "durationMax": "3.00 ms",
    "durationMean": "3.00 ms",
    "bytesIn": 0,
    "bytesOut": 4446,
    "count": 1,
    "srcNameAggr": "pvt",
    "srcNamespace": "-",
    "srcType": "net",
    "destServiceName": "",
    "destServiceNamespace": "",
    "destServicePort": 0,
    "destNameAggr": "store-admin-d79444675-*",
    "destNamespace": "pets",
    "destType": "wep",
    "method": "GET",
    "userAgent": "Python-urllib/3.11",
    "url": "4.246.54.60/products",
    "responseCode": "200",
    "type": "HTTP/1.1",
    "host": "aks-nodepool1-15264788-vmss000002"
}
```