# Introduction

BB wants a web application that can assist them in storing Quote, sales, accounting, and engineering data. They want to be able to quote multiple times, win bids, and create 3D models from the same data. As the database grows, they want to query the db to make predictions and reports for the business.

In the long term, they want this system to be customizable enough to use for any other business in the same industry.

Currently they have created an Engineering tool that runs in Net6 winforms on a desktop. This program is complex, and they want to retain the work used here.

Extras: The system should look good, be responsive, have the ability to display 3D models online.

# Initial Thoughts

### Stack

FARM (FastAPI, React, MongoDB)
ASP.Net - Port the current engineering software to it's own AWS EC2 server instance, and call to it through a very simple API.

REACT - Currently the newest and most wanted framework for creating interactive UI's that render quickly. React is becoming the most popular Front-End framework on the web.

FastAPI - Python powered API creation framework that will relay the data and traffic between the UI, DB, and ASP engineering app. While this API is younger, it is the fastest API available, and makes documentation very easy with it's built in tools. It is lightweight and does not carry the bloated feel of django and flask.

MongoDB - This is a noSQL (not only SQL) database framework that uses "document" based record groups. This is our favorite framework for data that needs to be flexible. BB is young in this project, and it is likely they will continue to grow their datafields. Mongo makes this easier than other DB solutions. It is similar to DynamoDB from AWS, which is also a fantastic option. Mongo is very popular and well supported.

## UI Design
Building on React, there is no limit. Feel free to share sample websites that you like.

## API Design

```json
{
  "quote": {
    "endpoints": {
      "getById": {
        "url": "/api/quote/{quote_id}",
        "method": "GET"
      },
      "create": {
        "url": "/api/quote",
        "method": "POST"
      },
      "update": {
        "url": "/api/quote/{quote_id}",
        "method": "PUT"
      },
      "delete": {
        "url": "/api/quote/{quote_id}",
        "method": "DELETE"
      }
    }
  },
  "customer": {
    "endpoints": {
      "getById": {
        "url": "/api/customer/{customer_id}",
        "method": "GET"
      },
      "create": {
        "url": "/api/customer",
        "method": "POST"
      },
      "update": {
        "url": "/api/customer/{customer_id}",
        "method": "PUT"
      },
      "delete": {
        "url": "/api/customer/{customer_id}",
        "method": "DELETE"
      }
    }
  },
  "order": {
    "endpoints": {
      "getById": {
        "url": "/api/order/{order_id}",
        "method": "GET"
      },
      "create": {
        "url": "/api/order",
        "method": "POST"
      },
      "update": {
        "url": "/api/order/{order_id}",
        "method": "PUT"
      },
      "delete": {
        "url": "/api/order/{order_id}",
        "method": "DELETE"
      }
    }
  }
}
```

### '/api/update'
```json

{
   "quote": {
      "quote_id": 1234,
      "quote_data": {
         "field1": "value1",
         "field2": "value2",
         "field3": "value3"
      }
   },
   "customer": {
      "customer_id": 5678,
      "customer_data": {
         "field1": "value1",
         "field2": "value2",
         "field3": "value3"
      }
   },
   "order": {
      "order_id": 9012,
      "order_data": {
         "field1": "value1",
         "field2": "value2",
         "field3": "value3"
      }
   }
}

```

## DB Design

### Customers
```json
{
  "id": "string", // Unique identifier for the customer
  "first_name": "string", // The first name of the customer
  "last_name": "string", // The last name of the customer
  "email": "string", // The email address of the customer
  "phone": "string", // The phone number of the customer
  "address": "string", // The address of the customer
  "city": "string", // The city where the customer lives
  "state": "string", // The state or province where the customer lives
  "country": "string", // The country where the customer lives
  "postal_code": "string", // The postal or zip code where the customer lives
  "created_at": "string", // The date and time the customer was created (in ISO 8601 format)
  "updated_at": "string" // The date and time the customer was last updated (in ISO 8601 format)
  "quotes":"quote[]" // List of quotes this customer has
  "orders":"order[]" // List of orders this customer has
}

```

### Quote
```json
{
  "id": "string", // Unique identifier for the order quote
  "order_id": "string", // Unique identifier for the order associated with the quote
  "quantity": "number", // The quantity of the quote being ordered
  "unit_price": "number", // The unit price of the quote being ordered
  "discount": "number", // The discount applied to the quote being ordered (as a percentage)
  "tax": "number", // The tax applied to the quote being ordered (as a percentage)
  "total_price": "number", // The total price of the quote being ordered (including discounts and taxes)
  "status": "string", // The status of the order quote (e.g. pending, fulfilled, cancelled)
  "created_at": "string", // The date and time the order quote was created (in ISO 8601 format)
  "updated_at": "string" // The date and time the order quote was last updated (in ISO 8601 format)
}
```

### Order
```json
{
  "id": "string", // Unique identifier for the sales order
  "quote_id": "string" // ID for the quote that generated this order
  "customer_id": "string", // Unique identifier for the customer associated with the sales order
  "order_date": "string", // The date the sales order was placed (in ISO 8601 format)
  "total_amount": "number", // The total amount of the sales order
  "discount": "number", // The discount applied to the sales order (as a percentage)
  "tax": "number", // The tax applied to the sales order (as a percentage)
  "status": "string", // The status of the sales order (e.g. pending, fulfilled, cancelled)
  "created_at": "string", // The date and time the sales order was created (in ISO 8601 format)
  "updated_at": "string" // The date and time the sales order was last updated (in ISO 8601 format)
}
```
