file = open("testfile.txt","w") 
import requests,json,datetime
from datetime import datetime

api_key = 'd35df6d443a1468e8c1c6f61763dad7d'
location = input("Enter the city name: ")

complete_api_link = "https://api.openweathermap.org/data/2.5/weather?q="+location+"&appid="+api_key
api_link = requests.get(complete_api_link)
api_data = api_link.json()

temp_city = ((api_data['main']['temp']) -273.15)
weather_desc = api_data['weather'][0]['description']
hmdt = api_data['main']['humidity']
wind_spd = api_data['wind']['speed']
date_time = datetime.now().strftime("%d %b %Y | %I:%M:%S %p")

file.write("---------------------------------------------------------------")
file.write("Weather Stats for -{}  || {}".format(location.upper(), datetime))
file.write("---------------------------------------------------------------")

file.write("Current temperature is: {:.2f} deg C".format(temp_city))
file.write("Current weather desc  :",weather_desc)
file.write("Current Humidity      :",hmdt, '%')
file.write("Current wind speed    :",wind_spd ,'kmph')
file.close()
