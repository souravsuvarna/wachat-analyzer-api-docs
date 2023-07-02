
WhatsApp Chat Analyzer API
====================
Welcome to the WhatsApp Chat Analyzer API Documentation

## Introduction

The WhatsApp Chat Analyzer API is a powerful tool specifically designed for frontend enthusiasts who are interested in building a **WhatsApp Chat Data Visualizer** project. Built on FastAPI, this API offers a seamless and efficient method to process chat data and returns the processed result data in JSON format.
<br/>

## Getting Started
### Installation
```
No need of any Installation.
```

### Authentication
```
No need of any Authentication.
```
<br/>

## API Usage

### Base URL

https://wachatanalyzer.onrender.com

<br/>

### Request Format

- POST <br>

***Example*** 

```
with open("filename.txt", "rb") as file:
    files = {"file": file}
    response = requests.post(url, files=files)
```
<br/>

### Response Codes
 >  200 OK: The request was successful <br>
 
 > 404 Not Found: The requested resource was not found.
 
<br/>

### Response Body
>>>>>>***Sample JSON***
```json
{
  "user": "jhon",
  "message": "hello", 
  "year": 2020,
  "month": "August",
  "day": 24,
  "hour": 8,
  "minute": 45,
  "seconds": 33,
  "dayname": "Monday"
}
```

## Endpoints
 1. ## **/upload**: <br/>

    URL: https://wachatanalyzer.onrender.com/upload
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, .txt file
    
    **Description**: This endpoint receives a WhatsApp Chat .txt file and returns processed data in **JSON** format. **Later this particular **JSON** will be passed to the rest all endpoints**.
    <br/>

    
>***Python Example:***
>>   ```
    url = "https://wachatanalyzer.onrender.com/upload"
    with open("filename.txt", "rb") as file:
        files = {"file": file}
        response = requests.post(url, files=files)
    json_data = response.json()
>    ```

>**Response Sample** :
>>>```json
{
 "Main": [
     { 
      "user": "jhon",
      "message": "hello", 
      "year": 2020,
      "month": "August",
      "day": 24,
      "hour": 8,
      "minute": 45,
      "seconds": 33,
      "dayname": "Monday"
      "month_num": 8
      },
      {
      "user": "Chris",
      "message": "Morning", 
      "year": 2020,
      "month": "August",
      "day": 24,
      "hour": 9,
      "minute": 25,
      "seconds": 03,
      "dayname": "Monday"
      "month_num": 8
      },
      {  
        '''
      }
  ]
}

<br/>

 2. ## **/group-memebers**: <br/>

    URL: https://wachatanalyzer.onrender.com/group-memebers
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json
    
    **Description**: This endpoint receives previously returned **JSON**(i.e "Main")  And returns list of members of group in JSON format. In this list the first field is **Overall Group** which can be used as parameter for the entire group analysis, and other particular member name can be used as the parameter for respective  individual analysis. 
    <br/>
    
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/group-members"
response = requests.post(url, json=json_data)
>    ```

>**Response Sample** :
>>>```json
[
  {
    'username': 'Overall Group'
  },
  {
    'username': 'Moein'
  },
  {
    'username': 'John'
  },
  {
    'username': 'Michel'
  },
  {
    'username': 'Chris'
  },
  {
    'username': 'Root'
  },
  {
    'username': 'Nick'
  },
  {
    'username': 'Starc'
  },
  {
    'username': 'Vin'
  }
]

<br/>

 3. ## **/fetch-stats**: <br/>

    URL: https://wachatanalyzer.onrender.com/fetch-stats
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json payload
    
    **Description**: This endpoint receives previously returned **JSON**(i.e "Main") and **username** as payload And returns json format of,<br>
    - Total Messages
    - Total Words
    - Media Shared
    - Link Shared
    
    <br/>
    
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/fetch-stats"
username="Overall Group"
payload = {
    "data": json_data,
    "username": username
}
response = requests.post(url,json=payload)
>    ```

>**Response Sample** :
>>>```json
{
    'Total Messages': 8078, 
    'Total Words': 30259, 
    'Media Shared': 1875, 
    'Link Shared': 79
}

<br/>

 4. ## **/overall-activity**: <br/>

    URL: https://wachatanalyzer.onrender.com/overall-activity
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json payload
    
    **Description**:  This endpoint receives previously returned **JSON**(i.e "Main") and **username** as payload, And returns json, Which consist **Date** and **Message** on that Date.  
    <br/>
    
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/overall-activity"
username="Overall Group"
payload = {
    "data": json_data,
    "username": username
}
response = requests.post(url,json=payload)
>    ```

>**Response Sample** :
>>>```json
[
    {
        'Date': '2020-02-07', 
        'Message': 56
    }, 
    {
        'Date': '2020-02-08', 
        'Message': 13
    }, 
    {
        'Date': '2020-02-10', 
        'Message': 27
    }, 
    {
        'Date': '2020-02-14', 
        'Message': 35
    }
]

<br/>

 5. ## **/top-active-members**: <br/>

    URL: https://wachatanalyzer.onrender.com/top-active-members
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json 
    
    **Description**:  This endpoint receives previously returned **JSON**(i.e "Main"), And returns the **User** and **Message** in decreasing order of number of **Message** in json format.
    **This endpoint only applicable for entire group analysis**.  
    <br/> 
    
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/top-active-members"
response = requests.post(url, json=json_data)
>    ``` 

>**Response Sample** :
>>>```json
[
    {
        'User': 'John', 
        'Message': 1788
    }, 
    {
        'User': 'Nick',
        'Message': 840
    }, 
    {
        'User': 'Mike,
        'Message': 828
    }, 
    {
        'User': 'Ryal',
        'Message': 753
    }
]

<br/>

 6. ## **/chat-percenatage**: <br/>

    URL: https://wachatanalyzer.onrender.com/chat-percentage
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json 
    
    **Description**:  This endpoint receives previously returned **JSON**(i.e "Main"), And returns the **User** and **Percentage** in decreasing order of number of **Percenatge** in json format.
    **This endpoint only applicable for entire group analysis**.  
    <br/> 
    
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/chat-percentage"
response = requests.post(url, json=json_data)
>    ``` 

>**Response Sample** :
>>>```json
[
    {
        'User': 'Osama', 
        'Percentage': 22.13
    }, 
    {
        'User': 'Varshini Kotian',
        'Percentage': 10.4
    }, 
    {
        'User': 'Ranju😺💙',
        'Percentage': 10.25
    }, 
    {
        'User': 'Ryal_rafter',
        'Percentage': 9.32
    }
]

<br/>


 7. ## **/monthly-activity**: <br/>

    URL: https://wachatanalyzer.onrender.com/monthly-activity
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json payload 
    
    **Description**:  This endpoint receives previously returned **JSON**(i.e "Main") and **username** as payload, and returns the json which consist **Month** and **Message** in that month sent by selected user.
    <br/> 
    
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/monthly-activity"
username="Overall Group"
payload = {
    "data": json_data,
    "username": username
}
response = requests.post(url,json=payload)
>    ``` 

>**Response Sample** :
>>>```json
[
    {'Month': 'January', 'Message': 202}, 
    {'Month': 'February', 'Message': 1383}, 
    {'Month': 'March', 'Message': 2018}, 
    {'Month': 'April', 'Message': 494}, 
    {'Month': 'May', 'Message': 519}, 
    {'Month': 'June', 'Message': 388}, 
    {'Month': 'July', 'Message': 816}, 
    {'Month': 'August', 'Message': 1632}, 
    {'Month': 'September', 'Message': 173}, 
    {'Month': 'October', 'Message': 163}, 
    {'Month': 'November', 'Message': 40}, 
    {'Month': 'December', 'Message': 250}
]

<br/>

 8. ## **/weekly-activity**: <br/>

    URL: https://wachatanalyzer.onrender.com/weekly-activity
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json payload 
    
    **Description**:  This endpoint receives previously returned **JSON**(i.e "Main") and **username** as payload, and returns the json which consist **Week** and **Message** in that weekday sent by selected user.
    <br/> 
    
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/weekly-activity"
username="Overall Group"
payload = {
    "data": json_data,
    "username": username
}
response = requests.post(url,json=payload)
>    ``` 

>**Response Sample** :
>>>```json
[
    {'Day': 'Monday', 'Message': 1017}, 
    {'Day': 'Tuesday', 'Message': 879}, 
    {'Day': 'Wednesday', 'Message': 1183}, 
    {'Day': 'Thursday', 'Message': 1054}, 
    {'Day': 'Friday', 'Message': 1057}, 
    {'Day': 'Saturday', 'Message': 1462}, 
    {'Day': 'Sunday', 'Message': 1426}
]

<br/>

 9. ## **/daily-activity**: <br/>

    URL: https://wachatanalyzer.onrender.com/daily-activity
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json payload 
    
    **Description**:  This endpoint receives previously returned **JSON**(i.e "Main") and **username** as payload, and returns the json which consist **Hour** and **Message** in that Hour sent by selected user.
    <br/> 
    
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/daily-activity"
username="Overall Group"
payload = {
    "data": json_data,
    "username": username
}
response = requests.post(url,json=payload)
>    ```

>**Response Sample** :
>>>```json
[
    {'Hour': 0, 'Message': 52}, 
    {'Hour': 1, 'Message': 3}, 
    {'Hour': 2, 'Message': 6}, 
    {'Hour': 3, 'Message': 1}, 
    {'Hour': 4, 'Message': 4}, 
    {'Hour': 5, 'Message': 1}, 
    {'Hour': 6, 'Message': 35}, 
    {'Hour': 7, 'Message': 54}, 
    {'Hour': 8, 'Message': 311}, 
    {'Hour': 9, 'Message': 199}
    {'''}
]

<br/>


10. ## **/num-of-media-shared**: <br/>

    URL: https://wachatanalyzer.onrender.com/num-of-media-shared
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json 
    
    **Description**:  This endpoint receives previously returned **JSON**(i.e "Main"), And returns the **User** and **Media** in decreasing order of number of **Media** in json format.
    **This endpoint only applicable for entire group analysis**.
    <br/> 
   
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/num-of-media-shared"
response = requests.post(url, json=json_data)
>    ```
    
>**Response Sample** :
>>>```json
[
    {'User': 'Mike', 'Media': 291}, 
    {'User': 'John', 'Media': 268}, 
    {'User': 'Ryal', 'Media': 256}, 
    {'User': 'Starc', 'Media': 153}, 
    {'User': 'Nick', 'Media': 126}
]

<br/>


11. ## **/num-of-emoji-shared**: <br/>

    URL: https://wachatanalyzer.onrender.com/num-of-emoji-shared
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json 
    
    **Description**:  This endpoint receives previously returned **JSON**(i.e "Main"), And returns the **User** and **Emoji** in decreasing order of number of **Emoji** in json format.
    **This endpoint only applicable for entire group analysis**.
    <br/> 
    
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/num-of-emoji-shared"
response = requests.post(url, json=json_data)
>    ```

>**Response Sample** :
>>>```json
[
    {'User': 'Mike', 'Emoji': 391}, 
    {'User': 'John', 'Emoji': 228}, 
    {'User': 'Ryal', 'Emoji': 216}, 
    {'User': 'Starc', 'Emoji': 153}, 
    {'User': 'Nick', 'Emoji': 116}
]

<br/>

12. ## **/most-emoji-shared**: <br/>

    URL: https://wachatanalyzer.onrender.com/most-emoji-shared
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json payload
    
    **Description**: This endpoint receives previously returned **JSON**(i.e "Main") and **username** as payload, and returns the json which consist **Emoji** and **Sent**  by selected user.
    <br/>  
    
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/most-shared-emojis"
username="Overall Group"
payload = {
    "data": json_data,
    "username": username
}
response = requests.post(url,json=payload)
>    ```

>**Response Sample** :
>>>```json
[
    {'Emoji': '🤣', 'Sent': 930}, 
    {'Emoji': '😂', 'Sent': 469}, 
    {'Emoji': '😆', 'Sent': 422}, 
    {'Emoji': '🔥', 'Sent': 231}, 
    {'Emoji': '🤦', 'Sent': 70}, 
    {'Emoji': '🥺', 'Sent': 60}, 
    {'Emoji': '💔', 'Sent': 60}, 
    {'Emoji': '🙄', 'Sent ': 55}, 
    {'Emoji': '👍', 'Sent': 52}
]

<br/>

13. ## **/late-night-chat-dat**: <br/>

    URL: https://wachatanalyzer.onrender.com/late-night-chat-data
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json 
    
    **Description**:  This endpoint receives previously returned **JSON**(i.e "Main"), And returns the **User** and **Messages** in decreasing order of number of **Messages** sent beween 23:00 to 3:00 in json format.
    **This endpoint only applicable for entire group analysis**.
    <br/> 
  
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/late-night-chat-data"
response = requests.post(url, json=json_data)
>    ```  

>**Response Sample** :
>>>```json
[
    {
        'User': 'John', 
        'Messages': 137
    }, 
    {
        'User': 'Nick', 
        'Messages': 49
    }, 
    {
        'User': 'Joseph',
        'Messages': 40
    }, 
    {
        'User': 'Chris',
        'Messages': 36
    }, 
    {
        'User': 'Vin', 
        'Messages': 32
    }
]

<br/>

14. ## **/early-morning-chat-data**: <br/>

    URL: https://wachatanalyzer.onrender.com/early-morning-chat-data
    
    HTTP Method: POST
    
    Response Format: JSON
    
    Parameters: url, json 
    
    **Description**:  This endpoint receives previously returned **JSON**(i.e "Main"), And returns the **User** and **Messages** in decreasing order of number of **Messages** sent beween 4:00 to 6:00 in json format.
    **This endpoint only applicable for entire group analysis**.
    <br/> 
   
>***Python Example:***
>>   ```
url = "https://wachatanalyzer.onrender.com/early-morning-chat-data"
response = requests.post(url, json=json_data)
>    ```  

>**Response Sample** :
>>>```json
[
    {
        'User': 'John', 
        'Messages': 137
    }, 
    {
        'User': 'Nick', 
        'Messages': 49
    }, 
    {
        'User': 'Joseph',
        'Messages': 40
    }, 
    {
        'User': 'Chris',
        'Messages': 36
    }, 
    {
        'User': 'Vin', 
        'Messages': 32
    }
]

<br/>

### Developed by

>The API was developed by [Sourav Suvarna](https://www.linkedin.com/in/souravsuvarna/)


### Open Source

>This API is open source and hosted on [GitHub](https://github.com/souravsuvarna/WhatsApp-Chat-Analyzer-API)


