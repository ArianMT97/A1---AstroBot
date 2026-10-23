# 🚀 Space Bot API Investigation Sheet

**Total Marks: 40**  
**TASK 1: Collect Required API Documentation**

This investigation sheet helps you gather key technical information from the three APIs required for the Space Bot project: **Webex Messaging API**, **ISS Current Location API**, **Weather API** and a **Geocoding API** , plus the Python time module. Also furhter investigate the application of Web Architecture and MVC design pattern in development of the Bot

---

##  Webex Messaging API (4 marks)

| Criteria | Details |
|---------|---------|
| API Base URL | `https://webexapis.com` |
| Authentication Method | `Bearer Token Authentication` |
| Endpoint to list rooms | `/v1/rooms` |
| Endpoint to get messages | `/v1/messages` |
| Endpoint to send message | `/v1/messages` |
| Required headers | `"Authorization": "Bearer (Token here), "Content-Type": "application/json", "Accept": "application/json"` |
| Sample full GET or POST request | `GET https://webexapis.com/v1/rooms, Headers: Authorization: Bearer (Token here), Accept: application/json` |

---

##  ISS Current Location API (2 marks)

| Criteria | Details |
|---------|---------|
| API Base URL | `http://api.open-notify.org` |
| Endpoint for current ISS location | `/iss-now.json` |
| Sample response format (example JSON) | `{"message": "success", "timestamp": 1792685841, "iss_position": {"longitude": "135.0001", "latitude": "26.2250"}}` |


---

##  Geocoding API (4 marks)

| Criteria | Details |
|---------|---------|
| Provider used | `OpenWeatherMap` |
| API Base URL | `http://api.openweathermap.org` |
| Endpoint for geocoding | `/geo/1.0/direct` |
| Endpoint for reverse geocoding | `/geo/1.0/reverse` |
| Authentication method | `API Key using the 'appid' query parameter` |
| Required query parameters | `Direct geocoding: q (city name/country, e.g. London,GB), appid (OpenWeather API key), Reverse geocoding: lat, lon, appid` |
| Sample request with latitude/longitude | `http://api.openweathermap.org/geo/1.0/reverse?lat=51.5098&lon=-0.1180&limit=5&appid={API key}` |
| Sample JSON response (formatted example) | `{"name": "London", "lat": 51.5098, "lon": -0.1180, "country": "GB"}` |


---


##  Weather API (3 marks)

| Criteria | Details |
|---------|---------|
| API Provider | `OpenWeatherMap` |
| API Base URL | `https://api.openweathermap.org` |
| Endpoint for current weather | `/data/2.5/weather` |
| Authentication method | `API Key using the 'appid' query parameter` |
| Required query parameters | `lat, lon, appid` |
| Sample JSON response (formatted example) | `{"weather": [{"description": "moderate rain"}], "main": {"temp": 12.5, "humidity": 81}, "wind": {"speed": 4.2},"name": "London", "sys": {"country": "GB"}}` |


---

##  Epoch to Human Time Conversion (Python time module) (2 marks)

| Criteria | Details |
|---------|---------|
| Library used | `time` |
| Function used to convert epoch | `time.localtime()` |
| Sample code to convert timestamp | `See Code Below` |

```python
import time

timestamp = 1792691163

rTime = time.strftime(
    "%Y-%m-%d %H:%M:%S",
    time.localtime(timestamp)
)

print(rTime)
```                                                   

|||
|---------|---------|
| Output (human-readable time) | `2026-10-22 19:02:18` |

---

##  Extended Feature API ( 3 marks)

| Criteria | Details |
|---------|---------|
| API Provider | '_________' |
| API Base URL | `_______________________________` |
| Endpoint | `_______________________________` |
| Authentication method | `_______________________________` |
| Required query parameters | `_______________________________` |
| Sample JSON response (formatted example) |  
```

```
|

--- 

##  Evaluation – Web Architecture, MVC Design & Security 

In this section, evaluate how web technologies, architecture, and design patterns have been applied in your **AstroBot**. Your responses must relate directly to your implementation and include reflection on your design decisions.

---

###  Web Architecture – Client–Server Model (3 marks)

Explain how the client–server model applies to your AstroBot:

- Client: The user interacting with AstroBot through a Webex room. 
- Servers: Webex API server, OpenWeather API server, Open Notify ISS API server.
- When the user sends a command in the Webex room, AstroBot checks the latest message using the Webex Messaging API. If the command is /weather, the bot first uses the OpenWeather Geocoding API to convert the city name into latitude and longitude. These coordinates are then sent to the OpenWeather Weather API to retrieve current weather information. If the command is /iss, the bot retrieves the current ISS coordinates from the Open Notify API and then uses the OpenWeather Reverse Geocoding API to try to identify a nearby location. The returned JSON data is processed by AstroBot and formatted into a readable message. AstroBot then sends the response back to the Webex room using the Webex Messaging API.
- User → Webex → AstroBot → APIs → AstroBot → Webex → User


####  Security Considerations: (3 marks )
- AstroBot handles API keys and tokens by allowing them to be entered at runtime instead of requiring them to be stored directly in the source code. This reduces the risk of accidentally exposing credentials in the GitHub repository. The program also checks API response status codes before processing the returned data. For example, if the Webex room request does not return status code 200, the program prints an error and returns an empty list.
- Input validation is also used when processing commands. AstroBot only processes messages that begin with /, and unknown commands return the message Unknown command. Use /help. The /weather command also checks whether a city name has been entered before making the API request.
- To reduce excessive API requests, the bot waits five seconds between checks using time.sleep(5). This helps prevent unnecessary repeated requests to the Webex API.

---

###  RESTful API Usage in Your Application (3 marks )

- AstroBot uses REST APIs to communicate with Webex, OpenWeather and Open Notify. The bot uses HTTP GET requests to retrieve data and POST requests to send data.
- GET requests are used to retrieve Webex rooms, retrieve the latest Webex message, get city coordinates from the OpenWeather Geocoding API, retrieve current weather data, retrieve the current ISS position and reverse geocode the ISS coordinates.
- A POST request is used when AstroBot sends a message back to the selected Webex room.
- The APIs return data in JSON format. AstroBot uses response.json() to convert the JSON response into Python data. The program then selects the required values, such as temperature, humidity, wind speed, latitude and longitude, and formats them into readable messages before sending them to Webex. For example, the weather function accesses values such as weather['main']['temp'], weather['main']['humidity'] and weather['weather'][0]['description'].

#### Security Considerations: (2 marks)
- AstroBot checks API response status codes before trying to use the returned data. For example, the program checks whether response.status_code != 200 and returns an error message or None if the request was unsuccessful.
- The program also handles empty or invalid responses. For example, the geocoding functions return None if no location is found, and the weather function returns City not found. if the city cannot be matched.
- To avoid excessive API calls, AstroBot waits five seconds between Webex message checks using time.sleep(5). This reduces unnecessary repeated requests and helps lower the risk of reaching API rate limits.

---

###  MVC Design Pattern in AstroBot (3 Marks)

| Component   | Description and Example (Relate to your Bot) |
|------------|----------------------------------|
| **Model**  | The functions that retrieve and process the data from the APIs. For example get_weather(), get_city_coordinates(), get_iss_location() and reverse_geocode(). |
| **View**   | The messages shown to the user in the Webex room, such as help messages, weather information and ISS location information.  |
| **Controller** | The main() function which checks the user's command and decides which function to use. For example, /weather calls get_weather() and /iss calls get_iss_location() |

---

### 📝 Reflection and Evaluation ( 8 marks )

Reflect on your AstroBot (400 words):

- How effective is your bot in meeting the Astronomy Club’s needs?  
- What design decisions worked well?  
- What challenges did you face when integrating APIs?  
- What security risks did you identify and how were they handled?  
- How could your solution be improved in the future?  

---

 **Tip:** Link your answers directly to your code and examples for higher marks.
### Notes

- Use official documentation for accuracy (e.g. developer.webex.com, locationiq.com or Mapbox, open-notify.org or other ISS API).
- Be prepared to explain your findings to your instructor or demo how you retrieved them using tools like Postman, Curl, or Python scripts.

---

###  Total: /40
