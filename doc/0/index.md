# Introduction #

Here is a quick guide to get familiar with **craft ai**.

The material for this tutorial is a web application that will browse
[reddit](https://www.reddit.com/) posts and match the titles to the names of
state capitals from all over the world. When there is a match, the application
will connect to the [OpenWeatherMap](http://openweathermap.org/) API, retrieve
the current weather for the corresponding capital and display it on a map.

## Getting ready ##

### Requirements ###

- A modern browser such as Chrome 45, Firefox 39 or Safari 9,
- A GitHub account.

### Setup ###

Before running the tutorials, you will need to create your own craft ai project. 
Do not worry, the content is publicly available, you only need to make a personal 
copy that you can edit. To do so, simply follow these steps:

- go to the [craft ai workbench](http://workbench.craft.ai/),
- log in with your GitHub account,
- click on the **+** button next to the 'tutorials' project,

![fork the 'Tutorials' project](https://raw.githubusercontent.com/craft-ai/tutorials/master/doc/0/fork.jpg "Forking")

Now let's open the project you just created by clicking the **pencil** button.

![edit the 'Tutorials' project](https://raw.githubusercontent.com/craft-ai/tutorials/master/doc/0/edit.jpg "Editing")

From the project explorer that appears on the left of the page, open the `craft_project.json` file with the cog icon.
You will end up on the **settings** page which will display your personal `Application ID` and `Application secret` 
associated to your **craft ai** project. Keep those items handy since they will be needed to run the tutorials.

![screenshot of the project settings](https://raw.githubusercontent.com/craft-ai/tutorials/master/doc/0/project_json.jpg "Application/Secret")

## Running ##

### First launch ###

Open your browser and go to [www.craft.ai/tutorials](http://www.craft.ai/tutorials/) and
click the `Run` button. You will be prompted to fill in a form with the information about 

!['Tutorials' form](https://raw.githubusercontent.com/craft-ai/tutorials/master/doc/0/form.jpg "Form")

The first three fields have to do with your **craft ai** project: your user name (that is, your GitHub user name), the project name (`tutorials`) and the project branch (by default, `master`).

In the `Behaviors folder` field, put "bts/0". This means that the app will create its agents based on the behavior trees that are present in the folder "bts/0" of the project.

The last two fields are to be filled in with the `Application ID` and `Application secret` retrieved from your **craft ai**

Once submitted, the data will appear in the URL like this:

```
http://www.craft.ai/tutorials
  ?owner=<github_username>
  &project=tutorials
  &branch=master
  &folder=bts/0
  &appid=<craft_ai_app_id>
  &appsecret=<craft_ai_app_secret>
```
This way you can save the url and when hitting the "Run" button from there, the form will be
completed with your data and all you will need to do is hit "Submit".

### Playing around ###

You can play around with the app and see what happens. The controls are the following:

  - `Run` will start an instance and display the posts retrieved from reddit in the web page;
  - `Stop` will stop the currently running instance which will prevent retrieving and displaying any more content, and restore the page to its initial state;

### Under the hood ###

Here's how the application works:

1. A **craft ai agent** that we will call the `reddit manager` retrieves the
front page of a given subreddit via the `GetFrontPage` action;
2. If the reddit API returns results, the `reddit manager` will
  - display a summary of the posts returned as thumbnails in the web page,
  - and send the results to the `city manager` agent using
  [craft ai messaging system](http://doc.craft.ai/behaviors/messages/index.html#the-messaging-system);

3. The `city manager` agent will then
  - compare the results' titles with a list of capitals (`GetCapitals` action),
  - and for each capital matched
    - display the thumbnail in a dedicated column (`DisplayCityThumbnail` action),
    - and retrieve the weather and display it on a map (`DisplayCityWeather` action);
4. When all of the results have been run through, the `city manager` agent will notify the `reddit manager` agent;
5. The `reddit manager` agent will send a request for other posts in the subreddit, and the scenario plays again, until no more posts are found.

## Next step ##
In [tutorial 1](../1/index.html), you will get to create your own behavior tree!