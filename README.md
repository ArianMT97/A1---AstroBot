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
- Consider but not limiting to secure handling of API keys and tokens, API rate limiting, and Input validation (e.g., handling user commands safely), include examples from code where necessary to illustrate.

---

###  RESTful API Usage in Your Application (3 marks )

Explain how REST APIs are used in your AstroBot: 

- Describe how HTTP methods (GET, POST) are used  
- Explain how your bot interacts with APIs (Webex, Weather, ISS, Geocoding)  
- Describe how JSON responses are received and processed  

Note: Relate your explanation directly to your code for higher grade. 

#### Security Considerations: (2 marks)
- Check response status codes, Handling invalid or unexpected API responses, Avoiding excessive API calls

---

###  MVC Design Pattern in AstroBot (3 Marks)

Explain how the **Model–View–Controller (MVC)** pattern applies to your solution:
Provide a short example based on your implementation

| Component   | Description and Example (Relate to your Bot) |
|------------|----------------------------------|
| **Model**  |  |
| **View**   |  |
| **Controller** |  |

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
