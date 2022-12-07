# HTTP
For this project, we had to choose two APIs to get data and display the data on the page.  To get the data from APIs we used javascript fetch API to send the requests and receive responses. We used global fetch() method that provides an easy, logical way to fetch resources asynchronously across the network. <br>
This project was built with @DominicSimpson<br>
Our project https://github.com/fac26/Dominic_Natalia_http<br>
See in action https://fac26.github.io/Dominic_Natalia_http/<br>
World GeoData allows a user to search a country's data and provides upon request the data about the country: area, population, language, capital, currencies, borders etc.

<hr>

## 1. Write code that executes asynchronously

The method getWeather() the word “async” before a function means one simple thing: a function always returns a promise. Other values are wrapped in a resolved promise automatically. So, async ensures that the function returns a promise, and wraps non-promises in it. The keyword await makes JavaScript wait until that promise settles and returns its result. That doesn’t cost any CPU resources, because the JavaScript engine can do other jobs in the meantime: execute other scripts, handle events, etc.


    const getWeather = async (city) => {
      const data = await fetchData(getweatherAPIurl + city);
      if (data.message) {
        //catch block
        weatherEl.innerHTML = `${data.message} weather`;
      } else if(Array.isArray(data)&&data.length===0 || data.temperature==''){//404
        console.log(data)
        weatherEl.innerHTML = 'No data available';
      } else {
        renderWeather(capital, data);
      }
    };


## 2. Use callbacks to access values that aren't available asynchronously
We used renderWeather() callback function in getWeather async function. If there is no data available from API we displayed the appropriate message otherwise we accessed the values from the response and displayed them on the page

    const renderWeather = (city, data) => {
      weatherEl.innerHTML = '';
      const pf = document.createElement('p');
      const ps = document.createElement('p');

      pf.innerHTML = `It is a ${data.description.toLowerCase()} day in ${city}.`;
      ps.innerHTML = `The temperature is ${data.temperature}, wind speed is ${data.wind}.`;
      weatherEl.append(pf, ps);
    };
    
    

## 3. Use promises to access values that aren't available asynchronously
Promises are extremely powerful for handling asynchronous operations in JavaScript. When sending off requests to load third-party data or do other asynchronous work, using a Promise has helped us for telling our code to wait until the async work is done before continuing. In our project we used Promises to display a message instead of throwing an error if we received !response.ok

        .catch((error) => {
          if (error.status === 404) {
            console.log(error)
            return [];
          } else {
            return new Promise(resolve=> resolve({message: `Sorry, something went wrong from server side. ${error.message}`}));
          }
        });

## 4. Use the fetch method to make the HTTP requests and receive responses

    function fetchData (url) {
      const fetchedData = fetch(url);
      return fetchedData
        .then((response) => {
          if (response.ok) {
            return response.json();
          } else {
            return Promise.reject({
              status: response.status,
              statusText: response.statusText,
            });
          }
        })
        .then((data) => {
          return data;
        })
        .catch((error) => {
          if (error.status === 404) {
            console.log(error)
            return [];
          } else {
            return new Promise(resolve=> resolve({message: `Sorry, something went wrong from server side. ${error.message}`}));
          }
        });
    };

9. Configure the options argument of the fetch method to make GET and POST requests
10. Use the map array method to create a new array containing new values
11. Use the filter array method to create a new array with certain values removed
12. Access DOM nodes using a variety of selectors
13. Add and remove DOM nodes to change the content on the page
14. Toggle the classes applied to DOM nodes to change their CSS properties
15. Use consistent layout and spacing
16. Follow a spacing guideline to give our app a consistent feel
17. Debug client side JS in our web browser
18. Usr console.log() to help us debug our code
