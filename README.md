# Flight Spotlight

A project to see all flights in a area _in realtime_ by subscribing to updates to a geographic area. From a UTM / U-Space point of view, this includes querying flights in a DSS and a live feed. It uses CesiumJS to display the flight data in 3D .

## Self host / Installation

This project uses Node JS and Express JS, a Tile 38 server, and can connect to a DSS instance. If you are using a DSS instance, you will need a JWT token to connect to the airspace. For that, you will need a approved UTM / U-Space OAUTH server (e.g. [Flight Passport](https://www.github.com/openskies-sh/flight_passport)). The following steps are for self host / test. In these steps we will not connect to the DSS and turn off all authentication

1. In Github branch to `selfhost-testrun`, this brach turns off all identity and authentication capabilities. 
2. Clone the repository and use `npm install | npm i` 
3. Create a process.env file using `touch process.env`
   1. Take a look at the .env.sample file to fill in your details. You will need the Bing / Mapbox keys for basemaps, you can igonre the Identity and Authorization keys. 
4. Download a precompiled binary of the  [Tile 38](https://www.tile38.com) server for your system. You can follow the instructions [in the releases page](https://github.com/tidwall/tile38/releases). Sample for Linux below
   ```shell
   curl -L  https://github.com/tidwall/tile38/releases/download/1.19.5/tile38-1.19.5-linux-amd64.tar.gz -o tile38-1.19.5-linux-amd64.tar.gz
   tar xzvf tile38-1.19.5-linux-amd64.tar.gz
   cd tile38-1.19.5-linux-amd64
   ./tile38-server
   ```
5. Run the local server using `npm start`
6. Navigate to `http://local.test:5000/spotlight` to launch the application. You should see a globe and a control to input a Area of Interest (AOI)
7. Copy paste the GeoJSON from the importers [folder](https://www.github.com/openskies-sh/flight-spotlight/importers/aoi-example.geojson)
8. Open a new terminal window and navigate to the importers directory and type in `python import_flight_json.py` file to upload flight information and see it on a map.

### Additional details
Take a look at the raw [JSON file](https://www.github.com/openskies-sh/flight-spotlight/importers/aoi-example.geojson) for sample flight data. This file follows the format as specified in the Airtraffic data protoocol and has a series of observations. Every five seconds this data is uploaded to the server and shown on a map. 

In the production version there is a POST request to post this data in realtime. 


## Screenshots

Initial screen
![terrain1](https://i.imgur.com/hQ3LmFk.jpg)