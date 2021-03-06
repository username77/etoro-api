### Etoro trading API


##### Requirments:
- java 11 (JDK11)
- internet connection

##### Build executable jar
````
./gradlew build
````
##### Set your account credentials into Environment variables: LOGIN, PASSWORD
````
export LOGIN=yourusername
export PASSWORD=yourpassword
````
##### Start API server
````
 java -jar build/libs/etoro-api-0.0.1-SNAPSHOT.jar
````

### Using API server

In order to trade you have to add asset to watchlist first, then you can open or close positions with this asset.
Your watchlist will be persisted locally in the watchlist.json if you start the server from the project folder.

- API documentation http://localhost:8088/etoro-api/v2/api-docs
- add assets to watchlist http://localhost:8088/etoro-api/watchlist/
- open/close positions http://localhost:8088/etoro-api/positions/

### Example

### Buy BTC in Demo mode
1 Add btc to watchlist
````
 curl -X PUT \
   http://localhost:8088/etoro-api/watchlist/byId \
   -H 'Content-Type: application/json' \
   -H 'cache-control: no-cache' \
   -d '{
 	"param": "btc"
 }'
````
2 Open position 
````
curl -X POST \
  http://localhost:8088/etoro-api/positions/open \
  -H 'Content-Type: application/json' \
  -H 'mode: Demo' \
  -d '{
	"name": "btc",
	"type": "BUY",
	"amount": 100,
	"leverage": 2,
	"takeProfitRate": 13000,
	"stopLossRate": 8000
}'
````
##### Make sure that "takeProfit" and "stopLoss" have valid values.
#### Response:
````
{
    "date": "2020-02-22T12:28:53.574543",
    "requestToken": "a859ec38-12bd-41b2-87f3-205515f2d608",
    "errorMessageCode": 0,
    "notificationParams": null,
    "position": {
        "leverage": 2,
        "stopLossRate": 8000,
        "takeProfitRate": 13000,
        "amount": 100,
        "instrumentID": "100000",
        "positionID": "1621284697",
        "isBuy": true,
        "isTslEnabled": false,
        "view_MaxPositionUnits": 0,
        "view_Units": 0,
        "view_openByUnits": null,
        "isDiscounted": false,
        "viewRateContext": null,
        "openDateTime": "2020-02-22T11:28:53.3993309"
    }
}
````

### Close BTC position in Demo mode
````
curl -X DELETE \
  'http://localhost:8088/etoro-api/positions/close?id=1621284697' \
  -H 'mode: Demo'
````




