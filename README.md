# UFO_Sightings
# UFO Sightings
## Purpose
The client is a journalist interested in her home town McMinnville,  Oregon. The town is famous for UFO sightings. To help her with her research I created a webpage with a dynamic table where she can filter and view the UFO data, but sadly no McMinnville sightings were present in the data.

## Methods
1. Before starting. I created an index.html file and a static folder. In the static folder I created a folder to store the images for the website, a css file for the website styling, and a js file to store the app and the data files. 

### HTLM
2. In the assignment module I put together most of the HTML to format the website and table, but the results from the module only filtered for the date, so I added filters for the city, state, country, and shape. I also remove the filter, button because the new app will detect changes in the filters and automatically filter the data. I also made some additional stylistic changes.

```
                        <li class="list-group-item bg-dark">
                          <label for="date">Enter Date</label>
                          <input type="text" placeholder="1/10/2010" id="datetime" />
                        </li>
                        <li class="list-group-item bg-dark">                          
                          <label for="city">Enter City</label>
                          <input type="text" placeholder="roswell" id="city" /></li>
                        <li class="list-group-item bg-dark">
                          <label for="state">Enter state</label>
                          <input type="text" placeholder="nm" id="state" />
                        </li>
                        <li class="list-group-item bg-dark">                          
                          <label for="country">Enter Country</label>
                          <input type="text" placeholder="us" id="country" /></li>
                        <li class="list-group-item bg-dark">
                          <label for="shape">Enter Shape</label>
                          <input type="text" placeholder="light" id="shape" /></li>
```
### App
3. Towards the end of the app.js file I modified the event listener to listen for a change in the filters instead of the button click from the module.
```
d3.selectAll("input").on("change", updateFilters);
```
4. After the buildTable function I created a variable to store the filters.
```
var filters ={}
```
5. I created a function to update the filters. In this function I created a variable that stored an element that was changed using the d3.select(this) method, a variable that used .property to store the value of the changed element (logged it to the console), and a variable to store the id of the filter that was changed using .attr.  I used an if statement to add that filterId and value to the filters list if a filter value was entered and an else statement to clear that filter from the filters object. Then I called the filterTables() function to apply the filters and rebuild the table.

```
function updateFilters() {

  let changedElement = d3.select(this);
  let changedValue = changedElement.property("value");
  console.log(changedValue);
  let filterId = changedElement.attr("id");
  if (changedValue) {
    filters[filterId] = changedValue;
  }
  else {
    delete filters[filterId];
  }
    filterTable();
  
 }
```
6. Then I created the filterTable() function. I declared a variable that set the filtered data equal to the table data. Then I used the object.entries method to iterate though the data and collect any entries matching the filters. Then the function calls the buildTable function on the filteredData variable to rebuild the table.
```
  function filterTable() {
  
    var filteredData = tableData
    //taken from: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries#iterating_through_an_object
    Object.entries(filters).forEach(([key, value]) => {
      filteredData = filteredData.filter(row => row[key] === value);
    });
   buildTable(filteredData);
  }
```
## Results
View Website [UFO Sightings]( https://michelaz.github.io/UFO_Sightings/index.html)
![UFO Sightings thumbnail]()

### How to Filter the UFO Sightings Data Table:
The table will display all the data if not filters are added into the filter search form. If there is no data matching the value then the table will appear to be empty. The table can be filtered by one or more of the following: date, city, state, country, and/or UFO shape.
- To filter by date: type a date into the enter date input. Then hit enter on your keyboard.
![date filter]()

- To filter by city: type a city into the enter city input. Then hit enter on your keyboard.
![city filter]()

- To filter by state: type a state into the enter state input. Then hit enter on your keyboard.
![state filter]()

- To filter by country: type a country into the enter country input. Then hit enter on your keyboard.
![country filter]()

- To filter by UFO shape: type a shape into the enter shape input. Then hit enter on your keyboard.
![shape filter]()

### Summary:
The sample of data is too small to provide sufficient information evidence supporting the existence of aliens. There are also some errors in the data, for example, one entry has “downtown” as the duration. I think a good way to get more data would be to add an entry form to this website where people could post about their sightings and maybe even upload images/videos. Currently there are no data summary tables or charts to visualize trends in the data and with the data how it is now it would be difficult, but adding some consistency in the data entry would make that easier.

Another good feature would be to add in the ability for users to make accounts, so that they could comment their theories or opinions of these sightings. Maybe add a polling function too for users to give their opinion on if they think the sighting is fact or fancy.

I would also change some of the formatting. I’d like to make all the filter input boxes line up with each other. To make the page easier to navigate I would add make the page stationary and make the table scroll. The filters would probably be easier to use if they were searchable drop downs as well.
