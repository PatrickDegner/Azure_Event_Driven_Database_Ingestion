# EventbasedDatabaseIngestion
A Project for Event Driven Data Ingestion with Azure

![insertdata](https://user-images.githubusercontent.com/108484798/205463749-7c661305-b231-475f-af3f-435fa47df1c9.png)
![parsejson](https://user-images.githubusercontent.com/108484798/205463752-394aceea-da7d-4319-9b4c-99254073e95d.png)


![blobcontent](https://user-images.githubusercontent.com/108484798/205463742-0f557672-d2b8-441c-9004-775fa4706b2f.png)

![deleteblob](https://user-images.githubusercontent.com/108484798/205463743-9386e477-1fc4-419c-9ab2-fcaeda9bbbe2.png)

![eventgrid](https://user-images.githubusercontent.com/108484798/205463746-84cd95ca-0a44-4487-87a6-dc2b06aff8ac.png)

```sh
uriPath(triggerBody()?['data'].url)
```


```sh
{
    "properties": {
        "customer_id": {
            "type": "string"
        },
        "item_name": {
            "type": "string"
        },
        "item_price": {
            "type": "integer"
        },
        "order_amount": {
            "type": "integer"
        },
        "order_id": {
            "type": "string"
        },
        "payment_provider": {
            "type": "string"
        }
    },
    "type": "object"
}
```


```sh
uriPath(triggerBody()?['data'].url)
```
