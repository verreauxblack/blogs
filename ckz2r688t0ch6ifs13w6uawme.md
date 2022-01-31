## Failure Condition

We are introducing a new feature in the [DronaHQ](https://www.dronahq.com) Studio as a Failure condition. Failure condition deals with API's/GraphQL's/DB's both success and failure response.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643206967739/9TmEZWKJ7.png)

###  What is Failure Condition?
- It has three input and five keywords
- Inputs are Condition, Message, Code. 
    - *Condition* and *Message* box both accepts inline JavaScript within double curly braces ```{{ }}``` *example:* ```{{STATUSCODE >= 400}}```
    - *Code* accepts Alphanumeric All caps with underscore ```_``` *example:* ```CODE_400```
-  Keywords are
   1. OUTPUT - to access success response data.
   2. ERROR -  to access Failure response data.
   3. HEADERS - to access the latest API test's headers.
   4. STATUSCODE - to access the latest API test's status code.
   5. STATUSMESSAGE - to access the latest API test's status message.
- apart from the above keywords, other JavaScript keywords are available.
- DronaHQ gives users more access to handle the API response <br>

For example, you can write a condition to check the status code of the API response and you can add your custom message to display in the app.

### How Failure Condition is working?

Failure condition accepts more than one condition. If the first condition returns true then the remaining conditions won't execute. If the first condition returns false then the next condition will execute and so on. Message and Code will be used in [Bind data](https://community.dronahq.com/t/bind-data-using-connectors/781) and [Action flow](https://community.dronahq.com/t/understanding-action-flow/572)

### Why Failure Condition? 
- Have you ever worked with API? If yes, then you might know about the API's status code and response. Third-party APIs sometimes send an error response with a success status code 200. This situation is a bit harder to handle. But if you are working on DronaHQ this can be easily handled.
- Write your condition to check the status code and add a custom message to display in app

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643207149639/5hf_iQv1O.png)

- Not only the status code, but you can also check the response data. you might ask why we need to check response data? Because API responses are not having static data all the time. It might have dynamic data.
- Imagine, you are using weather API in your app. you want to display a warning message if the temperature is more than 22 deg Celsius. In this case, you can use failure condition to check the temperature, which helps to reduce your time and effort to achieve this logic.

In this example, http://api.weatherapi.com is used. 

- Add ```http://api.weatherapi.com/v1/current.json``` this endpoint in DronaHQ.
- Write failure condition like below


![failureCondition for weather api.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643212686775/iLFW-BRWI.png)
> - 1st condition checks the status code if the status code is less than 400 then 2nd condition will execute.

> - 2nd condition checks response data,  Condition is ```{{OUTPUT.current.temp_c>22}}``` if temperature is more than 22 deg Celsius, then the Message ```Temperature is {{OUTPUT.current.temp_c}}, Condition is {{OUTPUT.current.condition.text}}``` and Code will be used in app 

### Bind data Result: 

![bind_data.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643608933895/poqu_k5Dt.png)

### Actionflow configuration.

![action_flow.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643607906424/gtqzurEEq.png)
>  if temperature is higher than 22 then Error branch will execute. otherwise success branch will execute 

**Action flow result: **


![actionflow_ result.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643608808271/IgQJM8R6W.png)
Want to learn more about Failure Condition? Check our [official document](https://community.dronahq.com/t/failure-response/1008) 