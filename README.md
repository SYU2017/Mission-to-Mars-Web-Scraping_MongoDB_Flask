# Week13-Web-Scraping_Mongo_Flask
 
 Mission to Mars

## Build a web application that scrapes various websites for data related to the Mission to Mars and displays the information in a single HTML page. 

### Flask API data visualization: Run "python app.py" using Conda commend line.
http://127.0.0.1:5000/


![picture](Image/mission_to_mars.png)


![picture](Image/weatherMars.png)


![picture](Image/imageMars.png)

The following outlines what you need to do.


## Step 1 - Scraping----`mission_to_mars.ipynb` 

Complete  initial scraping using Jupyter Notebook, BeautifulSoup, Pandas, and Requests/Splinter.

* Create a Jupyter Notebook file called `mission_to_mars.ipynb` and use this to complete all of your scraping and analysis tasks. 

### NASA Mars News

* Scrape the [NASA Mars News Site](https://mars.nasa.gov/news/) and collect the latest News Title and Paragragh Text. Assign the text to variables that you can reference later.

### JPL Mars Space Images - Featured Image

* Visit the url for JPL's Featured Space Image [here](https://www.jpl.nasa.gov/spaceimages/?search=&category=Mars).

* Use splinter to navigate the site and find the image url for the current Featured Mars Image and assign the url string to a variable called `featured_image_url`.

### Mars Weather

* Visit the Mars Weather twitter account [here](https://twitter.com/marswxreport?lang=en) and scrape the latest Mars weather tweet from the page. Save the tweet text for the weather report as a variable called `mars_weather`.

### Mars Facts

* Visit the Mars Facts webpage [here](http://space-facts.com/mars/) and use Pandas to scrape the table containing facts about the planet including Diameter, Mass, etc.

* Use Pandas to convert the data to a HTML table string.

### Mars Hemisperes

* Visit the USGS Astrogeology site [here](https://astrogeology.usgs.gov/search/results?q=hemisphere+enhanced&k1=target&v1=Mars) to obtain high resolution images for each of Mar's hemispheres.

* You will need to click each of the links to the hemispheres in order to find the image url to the full resolution image.

* Save both the image url string for the full resolution hemipshere image, and the Hemisphere title containing the hemisphere name. Use a Python dictionary to store the data using the keys `img_url` and `title`.

* Append the dictionary with the image url string and the hemisphere title to a list. This list will contain one dictionary for each hemisphere.

## Step 2 - MongoDB and Flask Application----`scrape_mars.py` and `app.py` and  `index.html`/templates

Use MongoDB with Flask templating to create a new HTML page that displays all of the information that was scraped from the URLs above.

* Start by converting your Jupyter notebook into a Python script called `scrape_mars.py` with a function called `scrape` that will execute all of your scraping code from above and return one Python dictionary containing all of the scraped data.

* Next, create a route called `/scrape` that will import your `scrape_mars.py` script and call your `scrape` function.

  * Store the return value in Mongo as a Python dictionary.

* Create a root route `/` that will query your Mongo database and pass the mars data into an HTML template to display the data.

* Create a template HTML file called `index.html` that will take the mars data dictionary and display all of the data in the appropriate HTML elements. 


## Hints

* Use splinter to navigate the sites when needed and BeautifulSoup to help find and parse out the necessary data.

* Use Pymongo for CRUD applications for your database. For this homework, you can simply overwrite the existing document each time the `/scrape` url is visited and new data is obtained.

* Use Bootstrap to structure your HTML template.

*  "Jinja2 template variable if None Object set a default value" following is one of the solutions learned from Stackoverflow:
    
       Use the none builtin function (http://jinja.pocoo.org/docs/templates/#none):

             {% if mars is not None %}   
             {{ mars.mars_hemisphere[i].image_url }}
             {% else %}
              NONE
             {%endif %}
             or   {{ mars.mars_hemisphere[i].image_url if mars != None else 'NONE' }}
             or if you need an empty string:

              {{ mars.mars_hemisphere[i].image_url  if mars != None }}

*  There’s also a simpler way to put the table in HTML: {{mars.mars_facts|safe}} -- mars is my dictionary with all the scraped data, and mars_facts is the “html” table created from scraping. All you need to do in the HTML is: {{mars.mars_facts|safe}} That will read in the HTML from mars_facts and interpret the HTML tags and display the table. 
