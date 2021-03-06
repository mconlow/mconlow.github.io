---
published: true
layout: post
date: "2016-04-29 10:19:58 -0500"
categories: tech
---

<!-- EXTERNAL LIBS-->

<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>

<script src="https://www.google.com/jsapi"></script>



<!-- EXAMPLE SCRIPT -->

<script>



// onload callback

function drawChart() {



var public_key = 'n1y4G2oxMxSOoNb7azNm';



// JSONP request

var jsonData = $.ajax({

url: 'https://data.sparkfun.com/output/' + public_key + '.json',

data: {page: 1},

dataType: 'jsonp',

}).done(function (results) {



var data = new google.visualization.DataTable();



data.addColumn('datetime', 'Time');

data.addColumn('number', 'Temp');





$.each(results, function (i, row) {

data.addRow([

(new Date(row.timestamp)),

parseFloat(row.temp)

]);

});



var chart = new google.visualization.LineChart($('#chart').get(0));



chart.draw(data, {

title: 'Mike Temperature Chart'

});



});



}



// load chart lib

google.load('visualization', '1', {

packages: ['corechart']

});



// call drawChart once google charts is loaded

google.setOnLoadCallback(drawChart);



</script>

## A Raspberry Pi Temperature Sensor

When I found out we were having a baby, I immediately clicked into gear and started [reading about how to raise an emotionally well-adjust 7-year old](https://play.google.com/store/books/details?id=APzgCL8mgHUC&source=productsearch&utm_source=HA_Desktop_US&utm_medium=SEM&utm_campaign=PLA&pcampaignid=MKTAD0930BO1&gl=US&gclid=CNm0mOCktcwCFUWbNwodFWAFBQ&gclsrc=ds). But I was also concerned that the baby's room would be too hot or cold and set out to make my, at the time, new Raspberry Pi into a temperature sensor. 

There are plenty of tutorials on the internet. I am pushing the data to Sparkfun, and visualizing it with Google Charts. Here is the live temperature in my bedroom (or whatever room the Raspberry Pi is currently in):

<div id="chart" style="width: 100%;"></div>




And just in case I tire of keeping the Raspberry Pi on all the time, here is a screen shot of it:

![]({{site.baseurl}}/images/temperature.png)
