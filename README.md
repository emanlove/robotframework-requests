[![Build Status](https://travis-ci.org/bulkan/robotframework-requests.png?branch=master)](https://travis-ci.org/bulkan/robotframework-requests)
[![PyPi downloads](https://pypip.in/d/robotframework-requests/badge.png)](https://crate.io/packages/robotframework-requests/)

RequestsLibrary is a [Robot Framework](http://code.google.com/p/robotframework/) test library that uses the [Requests](https://github.com/kennethreitz/requests) HTTP client.


Usage
=====

Install robotframework-requests via `pip`

```python
pip install -U robotframework-requests
```


Here is a sample test case.

|                           |                                  |                     |                                |                      |
| :------------------------ | :------------------------------- | :--------------     | :----------------------------- | :------------------- |
| Settings                  |                                  |                     |                                |
| Library                   | Collections                      |                     |                                |
| Library                   | RequestsLibrary                  |                     |                                |
| Test Cases                |                                  |                     |                                |
| Get Requests              |                                  |                     |                                |
|                           | Create Session                   | github              | http://api.github.com          |
|                           | Create Session                   | google              | http://www.google.com          |
|                           | ${resp}=                         | Get Request         | google                         | /                    |
|                           | Should Be Equal As Strings       | ${resp.status_code} | 200                            |
|                           | ${resp}=                         | Get Request         | github                         | /users/bulkan        |
|                           | Should Be Equal As Strings       | ${resp.status_code} | 200                            |
|                           | Dictionary Should Contain Value  | ${resp.json()}      | Bulkan Savun Evcimen           |


RequestsLibrary, tries to follow the same API as requests. In the above example we load in the `RequestsLibrary` using the `Library` keyword.
To be able to distinguish HTTP requests to different hosts and for ease of creation of test cases, you need to create a `Session`. Internally
this will create a `request.Session` object.  The `Create Session` keyword accepts two arguments; 

    * _alias_ to identify the session later
    * _root url_ to the server

HTTP verbs are mapped keywords which accept two arguments.

    * _alias_ identifying the Session we created earlier. 
    * _URI_  to send the request to.

Above we create two Sessions one to the _github api_ and the other to _google_. Creating sessions doesn't send any requests.

After we create a Session we can send any of the following `Get, Post, Put, Patch, Options, Delete, and Head` requests. In the above example we send a 
GET request to the session with the alias _google_ and check the HTTP response code. Then send a another GET request but this time to the session with 
the alias _github_ and pass in a `uri`. In this case it is `/users/bulkan` which will return a JSON string. `RequestsLibrary` returned object provides 
a method to get the content as a JSON object format called json().

For more examples see the `tests` folder which contains testcase files that is used to test the keywords in this library against [httpbin.org](http://httpbin.org).


Documentation
=============

For individual keyword documentation see the following;

[http://bulkan.github.io/robotframework-requests/](http://bulkan.github.io/robotframework-requests/)

You can update the documentation once checked out by going to the top directory of this repo and issuing the following command:
python -m robot.libdoc src/RequestsLibrary/RequestsKeywords.py doc/RequestsLibrary.html


Help
====

Send your questions to the [Robot Framework Users Group](https://groups.google.com/forum/#!forum/robotframework-users)


[Follow me on twitter - @bulkanevcimen](https://twitter.com/bulkanevcimen)
