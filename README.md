![eventdriven](https://user-images.githubusercontent.com/108484798/205466499-4493ab47-7a4c-4fd0-8f4e-f9a5d767360b.jpg)

# Event driven Database Ingestion
A Project for Event Driven Data Ingestion with Azure

Want some live data in your database? This is just one of many ways created in Azure.

This is my Blog Post about this Project:

https://patricksdejourney.blogspot.com/2023/01/maximizing-efficiency-streamline-your.html

New data will become available in your database just milliseconds after the creation.

</br>

## How it works

I made a Python Tool to fake orders coming from an "fake-api" as json files and being uploaded to Azure Blob Storage

[This is my repo I have used](https://github.com/PatrickDegner/FakeOrderDatabaseEntry)

In this project I am using Azure Logic Apps with Event Grid to capture the Eventdata.

1. Data will be uploaded to a container
2. Event Grid will trigger the Workflow
3. The json file will be read and the data ingested into an Azure SQL Database

4. Profit! We have Live-Data in our Relational Database!


</br>

# How to use

Use the code of this repo or just follow along.

- Create a Logic app
- Create a SQL Database
- Create a Storage account


Create a table in your database.

This data is for testing only, thats why I also dont create any kind of database schema.

![table_create](https://user-images.githubusercontent.com/108484798/205465405-ec6b6f23-62a3-481a-890e-48715cb1679b.png)

Then the Eventgrid to find any change in the Blobstorage.

![eventgrid](https://user-images.githubusercontent.com/108484798/205463746-84cd95ca-0a44-4487-87a6-dc2b06aff8ac.png)

Next, the content of the blob will be read

Into Blobpath put the following
```sh
uriPath(triggerBody()?['data'].url)
```
This will find the new file in the container

![blobcontent](https://user-images.githubusercontent.com/108484798/205463742-0f557672-d2b8-441c-9004-775fa4706b2f.png)

Now we read the json file.
As Schema just use:
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

![parsejson](https://user-images.githubusercontent.com/108484798/205463752-394aceea-da7d-4319-9b4c-99254073e95d.png)

Data will be inserted into the Database.

Pick the right fields from the json output

![insertdata](https://user-images.githubusercontent.com/108484798/205463749-7c661305-b231-475f-af3f-435fa47df1c9.png)

Finally the processed json file will be deleted from blob.

Usually you would store it somewhere else to not lose this data ;)

This uripath is used again:
```sh
uriPath(triggerBody()?['data'].url)
```

![deleteblob](https://user-images.githubusercontent.com/108484798/205463743-9386e477-1fc4-419c-9ab2-fcaeda9bbbe2.png)

</br>

## How it looks like in action

In this gif you can see how I create 25 Orders. 1 every second.

The files will be pushed to Blob Storage and the Workflow will catch them and ingest into the Database.

You can push a file every millisecond if you want. The Workflow will pick them up and ingest.



![20221203_230520](https://user-images.githubusercontent.com/108484798/205464659-60d8d4ab-996f-40c1-8b3b-ae49d61716ad.gif)

