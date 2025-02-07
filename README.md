Selenium Requests
=================
Extends Selenium WebDriver classes to include the [request](http://docs.python-requests.org/en/latest/api/#requests.request) function from the [Requests](http://python-requests.org/) library, while doing all the needed cookie and request headers handling.

Before the actual request is made, a local HTTP server is started that serves a single request made by the webdriver instance to get the "standard" HTTP request headers sent by this webdriver; these are cached (only happens once during its lifetime) and later used in conjunction with the Requests library to make the requests look identical to those that would have been sent by the webdriver. Cookies held by the webdriver instance are added to the request headers and those returned in a response automatically set for the webdriver instance.


Features
--------
 * Determines and sends the default HTTP headers (User-Agent etc.) for the chosen WebDriver
 * Manages cookies bidirectionally between requests and Selenium
 * Switches to already existing window handles or temporarily creates them to work with the webdriver's cookies when making a request
 * All operations preserve the original state of the WebDriver (active window handle and window handles)
 * Tested to work with Selenium (3.0.1) using Mozilla Firefox (49.0.2), Google Chrome (54.0.2840.71) and PhantomJS (2.1.1)


Usage
-----
```python
# Import any WebDriver class that you would usually import from
# selenium.webdriver from the seleniumrequests module
from seleniumrequests import Firefox

# Simple usage with built-in WebDrivers:
webdriver = Firefox()
response = webdriver.request('GET', 'https://www.google.com/')
print(response)


# More complex usage, using a WebDriver from another Selenium-related module:
from seleniumrequests.request import RequestsSessionMixin
from someothermodule import CustomWebDriver


class MyCustomWebDriver(RequestsSessionMixin, CustomWebDriver):
    pass


custom_webdriver = MyCustomWebDriver()
response = custom_webdriver.request('GET', 'https://www.google.com/')
print(response)
```


Installation
------------
```pip install selenium-requests```
