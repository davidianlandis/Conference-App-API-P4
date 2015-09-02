# TASK 1 - sessions
	Sessions were implemented by creating a new "Session" entity
		With both a data model (a sub-class of ndb.model)
		And a request/ response model

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