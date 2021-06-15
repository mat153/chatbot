import spacy
import requests

nlp = spacy.load("en_core_web_lg")

def process_text(text):
    doc = nlp(text.lower())
    result = []
    for token in doc:
        if token.text in nlp.Defaults.stop_words:
            continue
        if token.is_punct:
            continue
        if token.lemma_ == '-PRON-':
            continue
        result.append(token.lemma_)
    return " ".join(result)

def funkcja(city):
    url = "http://api.openweathermap.org/geo/1.0/direct?q=" + city + "&limit=1&appid=89b52926bee9ddfc9ed8f938c7aaa84f"
    payload = ""
    headers = {}
    response = requests.request("GET", url, headers=headers, data=payload)
    response_json = response.json()[0]

    lat = response_json['lat']
    lon = response_json['lon']

    url = "https://api.met.no/weatherapi/locationforecast/2.0/compact?lat=" + str(lat) + "&lon=" + str(lon)
    headers = {'User-Agent': 'testappForStudyPurpose'}
    response = requests.request("GET", url, headers=headers, data=payload)
    response_json = response.json()
    sky_options = {
        "clearsky_day": "clear sky day",
        "clearsky_night": "clear sky night",
        "clearsky_polartwilight": "clear sky polar twilight",
        "cloudy": "cloudy",
        "fair_day": "fair day",
        "fair_night": "fair night",
        "fair_polartwilight": "fair polar twilight",
        "fog": "fog",
        "heavyrain": "heavy rain",
        "heavyrainandthunder": "heavy rain and thunder",
        "heavyrainshowers_day": "heavy rain showers day",
        "heavyrainshowers_night": "heavy rain showers night",
        "heavyrainshowers_polartwilight": "heavy rain showers polar twilight",
        "heavyrainshowersandthunder_day": "heavy rain showers and thunder day",
        "heavyrainshowersandthunder_night": "heavy rain showers and thunder night",
        "heavyrainshowersandthunder_polartwilight": "heavy rain showers and thunder polar twilight",
        "heavysleet": "heavy sleet",
        "heavysleetandthunder": "heavy sleet and thunder",
        "heavysleetshowers_day": "heavy sleet showers day",
        "heavysleetshowers_night": "heavy sleet showers night",
        "heavysleetshowers_polartwilight": "heavy sleet showers polar twilight",
        "heavysleetshowersandthunder_day": "heavy sleet showers and thunder day",
        "heavysleetshowersandthunder_night": "heavy sleet showers and thunder night",
        "heavysleetshowersandthunder_polartwilight": "heavy sleet showers and thunder polar twilight",
        "heavysnow": "heavy snow",
        "heavysnowandthunder": "heavy snow and thunder",
        "heavysnowshowers_day": "heavy snow showers day",
        "heavysnowshowers_night": "heavy snow showers night",
        "heavysnowshowers_polartwilight": "heavy snow showers polar twilight",
        "heavysnowshowersandthunder_day": "heavy snow showers and thunder day",
        "heavysnowshowersandthunder_night": "heavy snow showers and thunder night",
        "heavysnowshowersandthunder_polartwilight": "heavy snow showers and thunder polar twilight",
        "lightrain": "light rain",
        "lightrainandthunder": "light rain and thunder",
        "lightrainshowers_day": "light rain showers day",
        "lightrainshowers_night": "light rain showers night",
        "lightrainshowers_polartwilight": "light rain showers polar twilight",
        "lightrainshowersandthunder_day": "light rain showers and thunder day",
        "lightrainshowersandthunder_night": "light rain showers and thunder night",
        "lightrainshowersandthunder_polartwilight": "light rain showers and thunder polar twilight",
        "lightsleet": "light sleet",
        "lightsleetandthunder": "light sleet and thunder",
        "lightsleetshowers_day": "light sleet showers day",
        "lightsleetshowers_night": "light sleet showers night",
        "lightsleetshowers_polartwilight": "light sleet showers polar twilight",
        "lightsnow": "light snow",
        "lightsnowandthunder": "light snow and thunder",
        "lightsnowshowers_day": "light snow showers day",
        "lightsnowshowers_night": "light snow showers night",
        "lightsnowshowers_polartwilight": "light snow showers polar twilight",
        "lightssleetshowersandthunder_day": "lights sleet showers and thunder day",
        "lightssleetshowersandthunder_night": "lights sleet showers and thunder night",
        "lightssleetshowersandthunder_polartwilight": "lights sleet showers and thunder polar twilight",
        "lightssnowshowersandthunder_day": "lights snow showers and thunder day",
        "lightssnowshowersandthunder_night": "lights snow showers and thunder night",
        "lightssnowshowersandthunder_polartwilight": "lights snow showers and thunder polar twilight",
        "partlycloudy_day": "partly cloudy day",
        "partlycloudy_night": "partly cloudy night",
        "partlycloudy_polartwilight": "partly cloudy polar twilight",
        "rain": "rain",
        "rainandthunder": "rain and thunder",
        "rainshowers_day": "rain showers day",
        "rainshowers_night": "rain showers night",
        "rainshowers_polartwilight": "rain showers polar twilight",
        "rainshowersandthunder_day": "rain showers and thunder day",
        "rainshowersandthunder_night": "rain showers and thunder night",
        "rainshowersandthunder_polartwilight": "rain showers and thunder polar twilights",
        "sleet": "sleet",
        "sleetandthunder": "sleet and thunder",
        "sleetshowers_day": "sleet showers day",
        "sleetshowers_night": "sleet showersnight",
        "sleetshowers_polartwilight": "sleet showers polar twilight",
        "sleetshowersandthunder_day": "sleet showers and thunder day",
        "sleetshowersandthunder_night": "sleet showers and thunder night",
        "sleetshowersandthunder_polartwilight": "sleet showers and thunder polar twilight",
        "snow": "snow",
        "snowandthunder": "snow and thunder",
        "snowshowers_day": "snow showers day",
        "snowshowers_night": "snow showers night",
        "snowshowers_polartwilight": "snow showers polar twilight",
        "snowshowersandthunder_day": "snow showers and thunder day",
        "snowshowersandthunder_night": "snow showers and thunder night",
        "snowshowersandthunder_polartwilight": "snow showers and thunder polar twilight"
    }
    sky_code = response_json['properties']['timeseries'][0]['data']['next_1_hours']['summary']['symbol_code']
    sky_response = sky_options[sky_code]
    return 'It is ' + str(sky_response) + ', ' + str(
        response_json['properties']['timeseries'][0]['data']['instant']['details'][
            'air_temperature']) + ' Celsius degree'




weather_questions = ["I want to see a weather in", "What's the weather like?", "What’s it like out?",
                     "What’s the temperature?", "What’s the weather expected to be in the evening?",
                     "What’s the weather forecast?", "How is the weather today?", "How’s the weather?",
                     "I want weather"
                     ]

nlp.Defaults.stop_words.add("want")
nlp.Defaults.stop_words.add("really")
nlp.Defaults.stop_words.add("what's")
nlp.Defaults.stop_words.add("how")


print("Hello. How can I help you?")
text = input()

percent2 = []
percent_bez = []
percent_dobry = []

process = process_text(text)
doc1 = nlp(process)
doc_bez_proc = nlp(text)

for quest in weather_questions:
    process2 = process_text(quest)
    doc2 = nlp(process2)
    percent = doc1.similarity(doc2)
    if percent > 0.70:
        percent2.append(percent)

for quest in weather_questions:
    doc2 = nlp(quest)
    percent4 = doc1.similarity(doc2)
    if percent4 > 0.70:
        percent_dobry.append(percent4)

for quest2 in weather_questions:
    doc2 = nlp(quest2)
    percent3 = doc_bez_proc.similarity(doc2)
    if percent3 > 0.70:
        percent_bez.append(percent3)

print("---------------")
print(percent2)
print(percent_bez)
print(percent_dobry)

size = len(percent2)

#print(size)

if size > 0:
    print("OK.In which city?")
    city = input()
    print(funkcja(str(process_text(city))))
else:
    print("Sorry I don't recognise this sentece")
