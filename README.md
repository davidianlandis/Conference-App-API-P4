# TASK 1 - sessions
	Sessions were implemented by creating a new "Session" entity
		With both a data model (a sub-class of ndb.model)
		And a request/ response model
		Data types for the models:
			Date for date.
			Integer for start time so it can be sorted numerically (24hr).
			Integer for the data id since it creates/ stores integer ids for each entity.
			The rest are strings since they could contain any kind of characters.
			(Also included computed property - for the query problem (task 3b)).


	The following endpoints were created for sessions:
		1. createSession - creates a new session using the SessionForm model
		2. getConferenceSessions - returns all sessions for specified conference
		3. getConferenceSessionsByType - returns all sessions by type WITHIN a specified conference
		4. getSessionsBySpeaker - returns all sessions by speaker name ACROSS all conferences

	Endpoints utilize additional methods:
		1. _createSessionObject - creates a new session entity from the request
		2. _copySessionToForm - copies the data into the response object


# TASK 2 - Session Wishlist
	implemented two new endpoints:
		1. session/wishlist/{key} - to add or remove a session from user's wishlist
		2. session/wishlist/ - to return all sessions in that user's wishlist

# TASK 3a - Additional Queries
	implemented two additional queries as new endpoints:
		1. getConferencesByCity - specify a city and get all the conferences taking place there
		2. getConferencesBySeatsAvailable - returns conferences with at least that number of seats available

# TASK 3b - Query Problem
	QUERY: How to query for all non-workshops before 7pm?
	PROBLEM: An inequality filter can only be applied to ONE property
	SOLUTION: 
		Use ndb.ComputedProperty to create a new property in the model of the two inequality filters
		Then query for if that property is true

# TASK 4 - Add a Task
	implemented a set_featured_speaker task
	checks for more than 1 session for that speaker, 
	and adds to memcache as featured speaker.
	this task is added to the queue each time a session is added

	added a getFeaturedSpeaker endpoint method to return the
	featured speaker from memcache

# RUNNING THE APPLICATION
	1. Create a new google developers application at console.developers.google.com
		a. Copy the application name to the first line in app.yaml
		b. Create new oauth 2.0 credentials (APIs & auth -> Credentials)
		c. Copy the client ID to the replace the client ID in the following files of the application:
			1. settings.py
			2. static/js/app.js (to enable the front end)
	2. Navigate to http://[application-name].appspot.com/_ah/api/explorer
		a. Run getProfile first to add your google account to the data
		b. Now run the different endpoints from the API explorer or
		c. Interact with the front-end application at http://[application-name].appspot.com/