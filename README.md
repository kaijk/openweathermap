# openweathermap
This repositority provides templates and a script to create Current, Daily, Hourly, and Alerts `Sensors` for Home Assistant using a One-Call API-KEY from Openweathermap.

A REST Call to the Openweathermap API is used to create an HA entity called `openweathermap_report`. The JSON data from the REST Call is loaded into an entity attribute.  Then `template sensors` parse the attribute for their specific data. 

Entity naming conventions follow a mashup of the legacy Dark Sky and Openweathermap approaches.  That is, Dary Sky used temperature_0d, Openweathermap uses temp for temperature. This uses temp_0d.

The build is modular and completely controlled by the `createopenweather` shell script.  The script is a series of mostly `sed` commands that take master files, set the desired day or hour, and append them to the `openweathermap.yaml` package. If you don't like the naming convention, or wish to exclude certain weather attributes, just edit the openweathercurrent.yaml, openweatherhourly0.yaml or openweatherdaily0.yaml files.

You will need to edit `openweatherheader.yaml` to specify your ONE-CALL API_KEY, your Latitude and Longitude, your Units, and Language along with any elements you desire to exclude (for example minutely).  After editing, pasting the https:... string into a browser should return a JSON result.  

Icons are managed in their own, `openweathericons.yaml` file. There are keys in the current, dialy0 and hourly0 files that indicate where the icon entity should be included.  This allows easy remapping or adding of addtional icons in one place.

-----------------
Download the files into a directory like `/config/opw_elements`.  Running the `createopenweather` shell script then creates a HA `package` named `openweathermap.yaml` in `/config/packages/`.  For this to work your configuration.yaml file needs to have the line `packages: !include_dir_named packages`. See HA documentation for `packages`.

