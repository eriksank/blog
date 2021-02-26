# Why mobile first?

## You will need a web service layer

With a good team, it does not matter what you build first: a mobile app or a website.

With an average team, however, it makes a serious amount of difference. With an average team, you must go mobile first.

Why?

In order to supply services to a mobile app, you must build a set of API service functions on the server side. You have to do that, simply to make your mobile app function. Nowadays, the lingua franca for such API functions, is the message format JSON. Later on, it will not be hard to use this API to supply services to a web application. Therefore, mobile first, web application next, pretty much always works.

The other way around is not true.

Average developers generally do not build an API that will service the needs of the web application. Instead, they will typically do what their web framework tutorial has taught them. Typical frameworks such as Laravel and Django encourage the developer to code his application logic straight into the http request responders, amidst a cargo-cult smokescreen of totally misunderstood MVC (Model-View-Controller).

Hence, the average team will build logic that expect a http request as input and sends out HTML as output.

This is not suitable for a mobile app, which generally sends out a request typically in JSON format and expects data back, also in JSON format.

A good team knows about this and will ignore the misleading web framework tutorials. They will make sure to focus on building JSON APIs first, regardless of whether they are doing mobile first or web first.

An average team, however, will mess up big time.

It is actually a good way to assess the level of your team.

Do they experience big trouble when trying to add a mobile app to an existing website? If yes, then you know that they are mediocre.

## The term "MVC" means something else

By the way, what exactly did Trygve Reenskaug mean by "Models-Views-Controllers" in his 1978 publication by the same name?

https://zenodo.org/record/3676092

None of the Web framework publishers, such as Laravel or Django, has ever read the original 1979 publication. 


- **Controller:** a widget like the Windows start button with its popup menu. The user uses it to select which program you want to interact with.
- **View:** your client app. It is the app that the user selected by using the controller.
- **Model:** your server-side application that responds to requests by the view.


An example of an MVC situation in a website:


- **Controller:** the Windows start button
- **View:** the Firefox web browser
- **Model:** a bunch of python scripts invoked by an apache web server

Therefore, the term "View-Model" is a synonym for the term "Client-Server".

By the way, the browser's address bar is also a "Controller", because it also helps the user to select which application to run.

