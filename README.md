# ScoreSpaceAPI
A public leaderboard for ScoreSpace Jams


# How to use

## python
First you need to have installed **requests** library.
if you dont have installed **requests** use command in command prompt: `python3 -m pip install requests`

if you have everything installed you can copy the commented code below!

Note that this is code for python 3.x.x !


```python
import requests
import json



def setHighScore(user: str, data: dict) -> None:
	# makes a POST request to ScoreSpaceAPI with user and data(formated json)
	# user is your username on discord
	# data needs to be formated json, else it will throw an error to you
	try:
		# formating the dict to json
		data = json.dumps(data)
		r = requests.post(
			"http://localhost:7777/?user={user}&highscore={data}".format(user=user, data=data)
			)
		
	except Exception as e:
		# Something went wrong!
		print("Something went wrong! error: " + str(e))


def getHighScore(user: str) -> dict:
	# gets every data, we want to pick only users data
	# user can be only a string
	# getting all data here
	try:
		r = requests.get(
			"http://localhost:7777/"
			)

		# formating it into dict from json
		data = json.loads(r.content)

		# getting users data
		userdata = data[user]

		# getting the highscores and putting them into dictionary(user: score)
		highScores = dict(userdata["HighScore"])

		# returning the dictionary with high scores, yay!
		return highScores

	except Exception as e:
		# Something went wrong!
		print("Something went wrong! error: " + str(e))


# before you set the highscores you firstly need to get the data, otherwise all data will be deleted!
data = getHighScore("TestUser") # replace "TestUser" with your username

# modify the data to your liking
data["NewUser"] = 10 # setting "NewUser" a highscore

# then write the data back to api!
setHighScore("TestUser", data) # Replace "TestUser" with your own username


# yay! you just set a users highscore online!
# rest of your code can go BELOW this
# good luck!
```

