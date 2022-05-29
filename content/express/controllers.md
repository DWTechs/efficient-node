
# Controllers

As seen in the previous chapter, for every route you define a route-handler callback function (ie: a middleware) that will contain the code to compute a proper respponse.
In MVC pattern ths is exactly what a controller should do.
This is why we put this callback functions into a "controllers" folder.
It helps make things cleaner as your "routes" pages are just a catalog of routes with no code inside. and all the logici is separated in its own controller.