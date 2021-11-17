

# RESTFul API - Design guidelines

*source*: [Best Practices for REST API Design](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/) / [Pragmatic RESTFul API](https://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api) / [REST Good Practices](https://medium.com/hashmapinc/rest-good-practices-for-api-design-881439796dc9)



#### TL;DR

- APIs are first and foremost for developers. Make good documentation, make it user-friendly and simplify it.
- Use JSON as a payload. It is an acceptable format for all platforms.
- Use names to describe paths. A path represents an entity that is retrieved or manipulated.
- Use logical nesting at endpoints if an entity has complex nested elements.
- Use HTTP verbs to define operations. POST / GET / PUT / DELETE can be mapped to DB CRUD operations.
- Manage errors with descriptive messages and statuses.
- Allow filtering, sorting and paging.
- Always secure the ends. SSL, Authentication and Authorization.
- Cache data whenever possible to improve response time.
- Version endpoints. Allow the user to decide when to update to a new version.


### What is REST API?

REST stands for REpresentational State Transfer. It is an application programming interface that conforms to architectural constraints, such as stateless communication and cacheable data. It is not a protocol or a standard. Although REST APIs can be accessed through a number of communication protocols, most often they are called over HTTPS.


### Why is API design so important?

REST APIs are the face of any service and therefore must:

1. Be easy to understand so integration is straightforward.
2. Be well documented, so that semantic behaviors are understood (not just syntactic)
3. Follow accepted standards such as HTTP

Since calls are stateless, REST is useful in cloud applications. Stateless components can be freely redeployed in the event of failure, and they can scale-up to accommodate changes in load. This is because any request can be directed to any instance of a component; there can be nothing recorded that should be remembered by the next transaction in the application.


### The guidelines

The following guidelines serve as an API development guide to follow the most common web service practices.

#### Accept and reply with JSON

​JSON is a standard for transferring data and almost any technology can use it. There are other ways to transfer data, like XML, but not all technologies support it. JSON is easily manipulated at the client-side, especially browsers. It is also very efficient.

#### Use nouns instead of verbs in endpoint paths

The hierarchical structure of the REST must be a representation of all the entities provided by the API. Since HTTP requests have different operations, we can use them with endpoints to manipulate entities. We can see a direct relationship between CRUD operations and POST / GET / PUT / DELETE operations. It is suggested to use the plural nouns, to represent the collection of objects. Using an explicit Id that an operation will be done to an object in this collection.

#### Use logical nesting on endpoints

When designing endpoints, it should contain the same logical association between the pieces of information. If an object contains another, this should be represented by the line `/ main_object /: id / nested_object`. The logic doesn't need to be a mirror of what's in the database, but needs to represent the logic of how entities are handled. If one entity cannot exist without the other, endpoints must reflect this dependency.

#### Handle errors elegantly and return standard error codes

Errors should have consistent information about the problem that occurred and always be addressed, so that they don't bring down the API.

#### Allow filtering, sorting and paging

The database behind the API can be very large. Allowing filtering, sorting, and paging is good practice so that the API is not overloaded and responses can be returned quickly.

#### Maintain good security practices

Most communications concern private data. The use of SSL / TLS is strongly recommended. To make it more secure, authentication must ensure that only recognized users can make requests and authorization allows that only users with a specific role can manipulate information.

#### Caching data to improve performance

Some endpoints return the same information over and over again. It is suggested to use caching on these endpoints to improve performance. REST should be 'stateles' and the cache can use endpoint settings to know what cached information has been requested.

#### Versioning of our APIs

To facilitate the migration of applications to new API features, it is recommended that you manage different versions of the API. This way, client applications can decide when and how to update their API requests. In turn, the API can continue improving its features without worring about compatibility.


### Examples

`*The HTTP verb is represented by [ ]`

The User entity represents a user. Each user has a permission list, which could be empty if there are none.

- `   [GET] /users` : return the complete user list
- `   [GET] /users?active=true` : return the list of active users
- `   [GET] /users/{:id}` : return the user of id {:id}
- `  [POST] /users` : create a new user
- `   [PUT] /users/{:id}` : update user info from id {: id}
- `[DELETE] /users/{:id}` : erase user info from id {: id}
- `   [GET] /users/{:id}/permissions` : return permissions list of user from id {:id}
- `   [PUT] /users/{:id}/permissions` : change permissions list of user from id {:id}

The Course entity represents an education course. Each course is composed of sessions and these, of resources. A user can register for a complete course or a session. Registrations cannot be changed.

- `   [GET] /courses` : return the complete list of courses
- `   [GET] /courses?dateDebut="2021-05-01"&dateFin="2020-08-31" ` : return the list of courses that take place between startDate and endDate
- `   [GET] /courses/{:id}` : return the course of id {:id}
- `  [POST] /courses` : create a new course
- `   [PUT] /courses/{:id}` : update course info from id {:id}
- `[DELETE] /courses/{:id}` : erase course info from id {:id}
- `   [GET] /courses/{:id}/inscriptions` : return subscription list of course from id {:id}
- `  [POST] /courses/{:id}/inscriptions` : add a subscription to the course from id {:id}
- `[DELETE] /courses/{:id}/inscriptions/{:inscriptionId}`: erase subscription from id {:inscriptionId} of the course from {:id} 
- `   [GET] /courses/{:id}/sessions` : return the sessions list of course from id {:id}
- `   [GET] /courses/{:id}/sessions/{:sessionId}` : return session from id {:sessionId}, which belongs to the course from id {:id}
- `  [POST] /courses/{:id}/sessions` : create a new session that belongs to the course from id {:id}
- `   [PUT] /courses/{:id}/sessions/{:sessionId}` : update session info from id {:sessionId}, which belongs to the course from id {:id}
- `[DELETE] /courses/{:id}/sessions/{:sessionId}` : erase session info from id {:sessionId}, which belongs to the course from id {:id}
- `   [GET] /courses/{:id}/sessions/{:sessionId}/inscriptions` : return subscriptions list of session from id {:sessionId}
- `  [POST] /courses/{:id}/sessions/{:sessionId}/inscriptions` : add subscription to the session from id {:sessionId}
- `[DELETE] /courses/{:id}/sessions/{:sessionId}/inscriptions/{:inscriptionId}`: subscription from id {:inscriptionId} of the session from id {:id} 