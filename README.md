# Choropleth-Map

*A simple choropleth map*

This is an app that allows you to create a simple choropleth map.


...

**Home Page**

<img src="/ChoroplethMap.PNG" title="home page" alt="home page" width="500px">


---


## Table of Contents 

> Sections
- [Sample Code](#Sample_Code)
- [Installation](#installation)
- [Features](#features)
- [Contributing](#contributing)
- [Team](#team)
- [FAQ](#faq)
- [Support](#support)
- [License](#license)


---

## Sample Code

```javascript
// choropleth map
  var urlArr=[];
  var urlObj;
  
  var ajax1 = $.ajax({dataType:'json',
          url: url1,
          success: function(par){
            for(var i=0; i<par.length; i++){
              urlArr.push(par[i]);
            }
          }
         });
  
  var ajax2= $.getJSON(url2,function(par){
      urlObj= Object.assign(par);
  });
  
  $.when(ajax1,ajax2).done(function(){
    
    var w= 1000;
    var h= 600;
    var dataArr=[urlArr, urlObj];
    
    const tooltip= d3.select('body')
                     .append('div')
                     .attr('class','tooltip')
                     .attr('id','tooltip')
                     .style('opacity', 0);
    
    const svg= d3.select('body')
                 .append('svg')
                 .attr("height", h)
                 .attr("width", w);
    


    const minEdu = d3.min(dataArr[0],d=>d['bachelorsOrHigher']);
    const maxEdu = d3.max(dataArr[0],d=>d['bachelorsOrHigher']);
   

    const colorValues = d3.scaleThreshold()
                          .domain([3,12,21,30,39,48,57,66])
                          .range(["white","#b3ffb3","#80ff80","#33ff33","#00ff00","#00cc00","#009900","#008000","#004d00"]);
    var myArr=[];
    for(var y=0; y<urlObj["objects"]["counties"]["geometries"].length; y++){
      urlArr[y]["fips"];
      for(var d=0; d<urlArr.length; d++){
        if(urlObj["objects"]["counties"]["geometries"][y]["id"] == urlArr[d]["fips"]){
          myArr.push({fips: urlArr[d]["fips"], state: urlArr[d]["state"], area_name: urlArr[d]["area_name"], bachelorsOrHigher: urlArr[d]["bachelorsOrHigher"]});
        }
      }
    }
    
    const counties = svg.selectAll("path")
      .data(topojson.feature(dataArr[1], dataArr[1]["objects"]["counties"]).features)
      .enter()
      .append("path")
      .attr("d", d3.geoPath())
      .attr("class", "county")
      .attr("data-fips", (d,i)=>myArr[i]["fips"])
      .attr("data-state", (d,i)=>myArr[i]["state"])
      .attr("data-area_name", (d,i)=>myArr[i]["area_name"])    
      .attr("data-education", (d,i) => myArr[i]["bachelorsOrHigher"])
      .attr("fill", (d,i)=>colorValues(myArr[i]["bachelorsOrHigher"]))
      //.append('title')
      //.text((f,i)=>i+ " "+dataArr[0][i]["fips"] +" "+ dataArr[0][i]["area_name"])
      .on("mouseover", function(){
          tooltip.transition()
                 .duration(200)
                 .attr("data-education",d3.select(this).attr("data-education"))
                 .style("opacity",0.7);
          tooltip.html(d3.select(this).attr("data-area_name")+", "+ d3.select(this).attr("data-state") + " " + d3.select(this).attr("data-education")+"%")
                 .style("left", d3.event.pageX + 10 +"px")
                 .style("top", d3.event.pageY + 10 + "px");
      })
      .on("mouseout", function(){
          tooltip.transition()
                 .duration(200)
                 .style("opacity",0)
      });
    
    const leg= [["3%","#e6ffe6"],["12%","#80ff80"],["21%","#33ff33"],["30%","#00ff00"],["39%","#00cc00"],["48%","#009900"],["57%","#008000"],["66%","#004d00"]]; 
    
    var colorArray=["#e6ffe6","80ff80","#33ff33","#00ff00","#00cc00","#009900","#008000", "#004d00"];
    var textArray=["3%","12%","21%","30%","39%","48%","57%","66%"];
    
    const legend = svg.selectAll('.legend')
                  .data(colorArray)
                  .enter()
                  .append('g')
                  .attr('id','legend')
                  .attr("transform", "translate(600,-30)");  
          
    legend.append('rect')
          .attr('width', 35)                         
          .attr('height', 10)
          .attr("x", (f,i)=>i*30)
          .attr("y", 55)
          .style('fill', (f)=>f)
       
    var legend2= svg.selectAll('.legend2')
                    .data(textArray)
                    .enter()
                    .append('g')
                    .attr("transform","translate(600,0)");

    legend2.append('text')
          .attr("x", (f,i)=>i*30-1)
          .attr("y", 36)
          .attr("id", "lines")
          .text("|");  
    
    legend2.append('text')
          .attr("x", (f,i)=>(i*30)-10)
          .attr("y", 56)
          .style("font-size",12)
          .text((f,i)=>f);  
    
  })

```

---

## Installation

## Features
## Usage (Optional)
## Documentation (Optional)
## Tests (Optional)

## Contributing


## Team

> Contributors/People

| [**seansangh**](https://github.com/seansangh) |
| :---: |
| [![seansangh](https://avatars0.githubusercontent.com/u/45724640?v=3&s=200)](https://github.com/seansangh)    |
| [`github.com/seansangh`](https://github.com/seansangh) | 

-  GitHub user profile

---

## FAQ

- **Have any *specific* questions?**
    - Use the information provided under *Support* for answers

---

## Support

Reach out to me at one of the following places!

- Twitter at [`@sean13nay`](https://twitter.com/sean13nay?lang=en)
- Github at [`seansangh`](https://github.com/seansangh)

---

## Donations (Optional)

- If you appreciate the code provided herein, feel free to donate to the author via [Paypal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=4VED5H2K8Z4TU&source=url).

[<img src="https://www.paypalobjects.com/webstatic/en_US/i/buttons/cc-badges-ppppcmcvdam.png" alt="Pay with PayPal, PayPal Credit or any major credit card" />](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=4VED5H2K8Z4TU&source=url)

---

## License

[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

- **[MIT license](http://opensource.org/licenses/mit-license.php)**
- Copyright 2019 © <a>S.S.</a>
