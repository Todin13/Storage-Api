# Storage API 
This is a simpe REST API system using load balancing and cross platform as it's a docker compose.

## Installation and start of the app
Clone this repository to your local machine.\
Verify that docker desktop is open or verify you are connected to docker engine and compose then \
Open the terminal and paste 

	docker compose up -d 

-d is only if you want to run the docker compose in the back

## API Endpoints
### GET /keys
This endpoint retrieves the keys necessary to send data in the system wich are : \

	['product', 'count', 'price']

### GET /storage
This endpoint retrieves a list of items from the Redis set named 'inventory'. It returns a JSON response with the inventory details, including product names, counts, and prices.

Example Request:

	curl http://localhost:9000/storage

Attention the request musst be send from another terminal than the one were the app is running.\

Example Response:

	{
  		"inventory": [
  		{
		  "product": "Product1",
		  "count": "10",
		  "price": "50.00"
		},
		{
      		  "product": "Product2",
      		  "count": "5",
  		  "price": "25.00"
		}]
	}
	
	
### POST /storage
This endpoint allows you to add new items to the inventory. You need to send a JSON request body with the following keys: 'product', 'count', and 'price'. If the keys match the required keys, the data will be pushed to Redis, and a success response will be returned. If the keys do not match, an error response will be sent.

Example Request:

	curl -H "Content-Type: application/json" -X POST -d '{"product":"disk", "count":5, "price": 20}' http://localhost:9000/storage

Attention the request musst be send from another terminal than the one were the app is running.\
 
Example Success Response:

	{
	  {"product":"disk","count":5,"price":20} was pushed correctly 
	}
	

## Configuration
You can configure the redis port and other settings in the code to match your environment, the number of api for load balancing and the volumes.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Author
Todin13
