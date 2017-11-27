---
layout: post
title:  "Quick Templating with Mustache and JSON"
date:   2017-10-07 15:43:44 -0600
categories: Mustache json
author: "Jayson Capps"
---

<img class="img-thumbnail" src="/assets/img/blog/mustachejs-screenshot.png" />

When I started my position at the UNM School of Law I quickly discovered the challenge of organizing and keeping track of our academic course descriptions on our website. The descriptions where stored on our web server as individual static HTML pages and simply linked to. With the course description file count over 500, it was unmanageable. After meeting with the School of Law Registrar and Academic Dean it was clear that School of Law needed something more manageable and streamline.

I didn’t want to rely on PHP and needed a simple way to store data without MySQL. In addition, I needed something lightweight that could be easily parsed by JavaScript as well as read by a person. My research lead me to JSON. Using JSON as the data format was a good solution because it was simple, less verbose than XML and due to its minimal formatting, it is easy to read. I planned out my JSON data objects and values and made sure that my structure was formatted perfectly using the JSON validator, <a href="https://jsonlint.com/" target="_blank">JSONLint</a>. 

After organizing my JSON data into a series of nested objects by course type I needed something to parse the data. I learned about the JavaScript client-side templating solution, <a href="https://mustache.github.io/" target="_blank">Mustache.js</a>. Mustache.js is simple to setup, logicless, and allows a developer to build templates to flow the data onto a specified area of the HTML page. Mustache.js uses a script to pull in the data and iterate over the objects in the JSON file. Then the script places the data into the designated template area on the page that acts similar to a placeholder. Using a series of curly braces and hashtags, the template only displays specified objects and values from the JSON file. Please see an example of the markup and code below.

<h3>JavaScript to Load the JSON into the Template</h3>

{% highlight javascript %}
// MUSTACHE + HIDESEEK VARIABLES

$(function() {
	  // jQuery TO LOAD JSON DATA
      $.getJSON('/assets/data/all_courses.json', function(data) {
		  // DEFINING THE TEMPLATE SCRIPT
          var template = $('#course-script').html();
		  var html = Mustache.to_html(template, data);
		  // DIV PLACEHOLDER FOR THE JSON DATA
          $('#all_courses').html(html);
		  
          // HIDESEEK SEARCH - NOT PART OF MUSTACHE
          $('#search').hideseek({
		   nodata: 'No results found'
	  });
    });
});

{% endhighlight %}

<h3>HTML and Mustache.js Template</h3>


{% highlight html %}

<!-- DIV PLACEHOLDER -->
<div id="all_courses"> 
  <!-- START OF TEMPLATE -->
  <script id="course-script" type="text/template">
        <!-- LOOP OVER all_courses.json START -->
        {% raw %}
        {{#courses}} 
        
        <!-- COURSES OBJECT -->
    		
			<div class="contents list">
			
			<h2>First Year Class Courses</h2>
				
                <!-- #first_year DISPLAYS ALL OF THE FIRST YEAR CLASSES -->
                
				{{#first_year}} 
				<div class="panel">
					<button class="btn btn-default list-group-item" type="button" data-toggle="collapse" data-target="#{{id}}" aria-expanded="false" aria-controls="{{id}}">
					
						<span class="pull-left"><strong>{{title}}&nbsp;<span class="badge">{{frequency_key}}</span></strong></span>
						<span class="pull-right label label-first-year">{{type}}</span>
					
					</button>
					<div class="collapse" id="{{id}}">
						<div class="well">
							<h2>{{title}}</h2>
							<p><strong>Course Type:</strong> <em>{{type}}</em><br /><strong>Family:</strong> <em>{{family}}</em></p>
							
							<p><strong>Description:</strong></p>
							<div>
								{{#html}}
									{{{html}}}
								{{/html}}
								{{^html}}
									<p>See professor for course description.</p> 
								{{/html}}
							</div>
						</div>
					</div>
				</div>
				{{/first_year}}
        {{/courses}}
        {% endraw %}
    </script> 
</div>

{% endhighlight %}

Please see the UNM School of Law <a href="http://lawschool.unm.edu/academics/course-descriptions/index.html" target="_blank">course descriptions page</a> for the final project.



[mustache-main]: https://mustache.github.io/


