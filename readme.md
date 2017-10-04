
# Tempratuur sinds 1901

Ik heb gekozen om de tempratuur data te gebruiken voor mijn dataset.Ik ben opzoek gegaan naar een geschikte visualisatie voor deze data.

## Workflow

Ik ben als eerste opzoek gegaan naar een geschikte visualisatie voor de dataset. Het moest er eentje zijn die ook negatieve getallen kon laten zien. Toen ik deze gevonden had, moest ik de code gaan aanpassen om zo mijn eigen data er in te kunnen laden

###### Explore

De moeilijkheidsgraad zat hem voor mij in de JavaScript. Ik ben daar nog niet heel erg goed in, en in combinatie met D3 wat ook helemaal nieuw is voor mij, heeft dat voor nogal wat gevloek gezorgd. 

###### Process

## Hieronder staat de code zoals ik hem van de website van D3 heb gehaald.:


<!DOCTYPE html>
<svg width="960" height="500"></svg>
<script src="https://d3js.org/d3.v4.min.js"></script>
<script>

var svg = d3.select("svg"),
    margin = {top: 20, right: 20, bottom: 30, left: 50},
    width = +svg.attr("width") - margin.left - margin.right,
    height = +svg.attr("height") - margin.top - margin.bottom,
    g = svg.append("g").attr("transform", "translate(" + margin.left + "," + margin.top + ")");

var parseTime = d3.timeParse("%d-%b-%y");

var x = d3.scaleTime()
    .rangeRound([0, width]);

var y = d3.scaleLinear()
    .rangeRound([height, 0]);

var line = d3.line()
    .x(function(d) { return x(d.date); })
    .y(function(d) { return y(d.close); });

d3.tsv("data.tsv", function(d) {
  d.date = parseTime(d.date);
  d.close = +d.close;
  return d;
}, function(error, data) {
  if (error) throw error;

  x.domain(d3.extent(data, function(d) { return d.date; }));
  y.domain(d3.extent(data, function(d) { return d.close; }));

  g.append("g")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x))
    .select(".domain")
      .remove();

  g.append("g")
      .call(d3.axisLeft(y))
    .append("text")
      .attr("fill", "#000")
      .attr("transform", "rotate(-90)")
      .attr("y", 6)
      .attr("dy", "0.71em")
      .attr("text-anchor", "end")
      .text("Price ($)");

  g.append("path")
      .datum(data)
      .attr("fill", "none")
      .attr("stroke", "steelblue")
      .attr("stroke-linejoin", "round")
      .attr("stroke-linecap", "round")
      .attr("stroke-width", 1.5)
      .attr("d", line);
});

</script>

## Hieronder staat mijn aangepaste code

'''<!DOCTYPE html>
<svg width="960" height="500"></svg>
<script src="https://d3js.org/d3.v4.min.js"></script>
<script>

var svg = d3.select("svg"),
    margin = {top: 20, right: 20, bottom: 30, left: 50},
    width = +svg.attr("width") - margin.left - margin.right,
    height = +svg.attr("height") - margin.top - margin.bottom,
    g = svg.append("g").attr("transform", "translate(" + margin.left + "," + margin.top + ")");

//Hier specificeer om wat voor soort data het gaat.
var parseTime = d3.timeParse("%Y%m%d");

var x = d3.scaleTime()
    .rangeRound([0, width]);

var y = d3.scaleLinear()
    .rangeRound([height, 0]);

var line = d3.line()
    .x(function(d) { return x(d.date); })
    .y(function(d) { return y(d.temp); });

//hier roep je je CSV file aan waar je data in verwerkt is.
//hieronder roep je ook je 2 categorien uit je CSV bestand aan
d3.csv("assesment.csv", function(d) {
  d.date = parseTime(d.date);
  d.temp = +d.temp;
  return d;
}, function(error, data) {
  if (error) throw error;

  x.domain(d3.extent(data, function(d) { return d.date; }));
  y.domain(d3.extent(data, function(d) { return d.temp; }));

  g.append("g")
      .attr("transform", "translate(0," + height + ")")
      .call(d3.axisBottom(x))
    .select(".domain")
      .remove();

  g.append("g")
      .call(d3.axisLeft(y))
    .append("text")
      .attr("fill", "#000")
      .attr("transform", "rotate(-90)")
      .attr("y", 6)
      .attr("dy", "0.71em")
      .attr("text-anchor", "end")
      .text("Temprature");

  g.append("path")
      .datum(data)
      .attr("fill", "none")
      .attr("stroke", "steelblue")
      .attr("stroke-linejoin", "round")
      .attr("stroke-linecap", "round")
      .attr("stroke-width", 1.5)
      .attr("d", line);
});

</script>'''

Zoals je ziet heb ik de d3.timeParse aangepast van ("%d-%b-%y") naar ("%Y%m%d"). Dit omdat het hier om Year, Month en Date gaat. Daarna heb ik de d3.tsv("data.tsv", aangepast naar d3.csv("assesment.csv", omdat mijn bestand een CSV file is.

Als laatste heb ik d.date = parseTime(d.date); en d.close = +d.close; aangepast naar d.date = parseTime(d.date); d.temp = +d.temp; omdat dit de de waardes binnen mijn CSV file aangeeft.

###### Review

Het was een erg moeilijke en stressvolle opdracht. Maar nu ik eenmaal weet hoe het precies moet vraag ik mezelf af waarom ik mij zo druk heb gemaakt. Ik vind wel dat je een beetje in het diepe wordt gegooid. Ik ben nog redelijke een leek als het gaat om JS en helemaal in combinatie met nieuwe dingen. Daarnaast vind ik dat we wel erg kort de tijd hebben voor bepaalde opdrachten.

[Line chart]: https://bl.ocks.org/mbostock/3883245

[Hulp]: https://github.com/d3/d3-time-format/blob/master/README.md#timeParse

[hulp]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#Calling_functions

[Data]: https://github.com/cmda-fe3/course-17-18/blob/master/assessment-1/temperature.csv

