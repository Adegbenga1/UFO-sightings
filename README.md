# UFO-sightings
## Overview
 In-depth analysis of UFO sightings that allow users to filter for multiple criteria at the same time.
 This analysis allow user to filter different attributes at this same time . It does provides opprotunity to 
 view different information simultaneiusly for better judgement.
 
 ## RESULTS
 <!DOCTYPE html>
<html lang="en">
<head>
  <link rel="stylesheet" href="static/css/style.css"></link>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>UFO</title>
  <link
      rel="stylesheet"
      href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css"
      integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm"
      crossorigin="anonymous"
    />
</head>
<body>
  <div class="wrapper">
    <nav class="navbar navbar-expand-lg">
      <nav class="navbar navbar-dark bg-dark navbar-expand-lg"></nav>
      <a class="navbar-brand" href="index.html">UFO Sightings</a>
    </nav>
  </div>
  <div class="jumbotron">
    <h1 class="display-8">The Truth is Out There</h1>
  </div>
  <div class="container-fluid">
    <div class="row">
      <div class="col-md-4"><h3>UFO Sightings: Fact or Fancy? <small>Ufologists Weigh In</small></h3></div>
      <div class="col-md-8">
        <p>Are we alone in the universe? For millennia, humans have turned to the sky to answer this question. 
          Now, thanks to research generously funded by W. Avy, a UFO-enthusiast and amateur ufologist, we can supplement 
          our sky-searching with data analysis."The release of this analysis is well-timed: It coincides with the 
          celebration of World UFO Day, which is a moment for ufologists around the world to connect, relax,
          and sample a range of UFO-themed snacks," said Dr. Ursula F. Olivier, the world's preeminent expert 
          on circular sightings."Citizen-scientists can be especially helpful in both cataloguing sightings—which is 
          hugely helpful for us in our search for aliens—and in helping us celebrate the work that has already been done,
          such as this data visualization project, which will help us raise awareness of the ubiquity of sightings!"
          Not everyone is ready to celebrate, however. Local CEO and vocal anti-alien activist V. Isualize reached 
          out to our reporters to go on record as firmly opposed to any attempts to provide access to this data. "If there are aliens, 
          they certainly would like to be left alone," she stated, before directing us to the Leave Aliens Alone (LAA) 
          community engagement initiative she founded and funds. So what do YOU think? 
          Are we alone in the universe? Are aliens trying to contact us, or do they want to be left alone? 
          Dig through the data yourself, and let us know what you see.
        </p>
      </div>
    </div>
  </div>
  <div class="container-fluid"></div>
    <div class="row">
      <div class="col-md-3">
        <form class="bg-dark">
          <p>Filter Search</p>
          <ul class="list-group bg-dark">
            <li class="list-group-item bg-dark">
              <label for="date">Enter Date</label>
              <input type="text" placeholder="1/10/2010" id="datetime" />
            </li>
            <li class="list-group-item bg-dark">
              <label for="city">Enter Date</label>
              <input type="text" class="form-control" placeholder="city" id="city" />
            </li>
            <li class="list-group-item bg-dark">
              <label for="state">Enter Date</label>
              <input type="text" class="form-control" placeholder="state" id="state" />
            </li>
            <li class="list-group-item bg-dark">
              <label for="country">Enter Date</label>
              <input type="text" class="form-control" placeholder="country" id="country" />
            </li>
            <li class="list-group-item bg-dark">
              <label for="shape">Enter Date</label>
              <input type="text" placeholder="shape" id="shape" />
            </li>
          </ul>
        </form>
      </div>
      <div class="col-md-9">
        <table class="table table-striped">
          <thead>
              <tr>
                  <th>Date</th>
                  <th>City</th>
                  <th>State</th>
                  <th>Country</th>
                  <th>Shape</th>
                  <th>Duration</th>
                  <th>Comments</th>
              </tr>
          </thead>
          <tbody></tbody>
        </table>
      </div>
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/d3/4.11.0/d3.js"></script>
  <script src="static/js/data.js"></script>
  <script src="static/js/app.js"></script>
</body>
</html>


app.js
// from data.js
const tableData = data;
// get table references
var tbody = d3.select("tbody");
function buildTable(data) {
  // First, clear out any existing data
  tbody.html("");
  // Next, loop through each object in the data
  // and append a row and cells for each value in the row
  data.forEach((dataRow) => {
    // Append a row to the table body
    let row = tbody.append("tr");
    // Loop through each field in the dataRow and add
    // each value as a table cell (td)
    Object.values(dataRow).forEach((val) => {
      let cell = row.append("td");
      cell.text(val);
    });
  });
}

// 1. Create a variable to keep track of all the filters as an object.
var filter = {}
//{idelementchanged:elementsvalue}
// 3. Use this function to update the filters. 
function updateFilters() {
  // 4a. Save the element that was changed as a variable.
  var changedElement = d3.select(this)
  // 4b. Save the value that was changed as a variable.
  var elementsValue = changedElement.property("value")
  console.log(elementValue);
  // 4c. Save the id of the filter that was changed as a variable.
  var  idElementChanged = changedElement.attr("id")
  console.log(filterId);
  // 5. If a filter value was entered then add that filterId and value
  // to the filters list. Otherwise, clear that filter from the filters object.
  if (elementsvalue){
    filter[idElementChanged] = elementsValue
  } else{
    delete filter[idElementChanged]
  }
  // 6. Call function to apply all filters and rebuild the table
  filterTable();
}
// 7. Use this function to filter the table when data is entered.
function filterTable() {
  // 8. Set the filtered data to the tableData.
  let filteredData = tableData
  // 9. Loop through all of the filters and keep any data that
  // matches the filter values
  Object.entries(filters).forEach(([key, value]) => {
    filteredData = filteredData.filter((row) => row[key] === value)
  });

  // 10. Finally, rebuild the table using the filtered data
  buildTable(filteredData);
}
// 2. Attach an event to listen for changes to each filter
d3.selectAll("input").on("click", updateFilters); 
// Build the table when the page loads
buildTable(tableData);

 ## RESULTS 
 Resuts showed mutiple filters for updating required information as necessary and needed
![image](https://user-images.githubusercontent.com/70987568/133015674-2d2b5622-d220-4e54-852a-a58c63e173fd.png)
