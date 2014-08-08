---
Description: Formatting function for JavaScript strings, by replacing elements in a the string using values passed in to the method.
Keywords:
- GO
Section: post
Slug: javascript-string-format
Tags:
- javascript
- html
Title: Foramtting function for JavaScript strings
Topics:
- javascript
- jquery
- html
date: 2014-08-08
---

The project I work on has been around for about 10 years now. Due to the nature of the work a lot of the updates that should happen don't due to how work is paid for. I am currently working on the task of taking our application that was mainly built and used by customers for IE 6 and making that work in all of the latest major browsers. As you can imagine there is a lot of problems that we are running into. 

One issue that I was dealing with recently was a large section of code that takes an array of JSON objects and pushes the data into a table. The code was building each row, cell and all the attribute individually in a loop, as well we use a lot of non-standard attributes on elements. Not only was this just not working and was not rebuilding the full table. 

I began trying to work out a solution where I could define a string representing the table row I was creating with the locations where I needed the data to be placed (think printf or any number of methods in many programming languages.) After several iterations I had a working solution but didn't want to have to call the function as much as I just wanted to apply the formatting to the string, the result is the function below.

{{% highlight javascript %}}
	String.prototype.format = function() {
	  var s = this.toString();
	  for (var i = 0; i < arguments.length; i++) {       
	    var reg = new RegExp("\\{" + i + "\\}", "gm");             
	    s = s.replace(reg, arguments[i]);
	  }

	  return s;
	}

{{% /highlight %}}

As you can see from the code we are replacing points in the strings formatted like this {1} with elements from the array. an actual string example would be like the section below for say making a table. Then simply call the rowTemplate.format(arguments) to have all your values inserted in to the string, and using jQuery insert the table into the DOM.

{{% highlight javascript %}}
	var rowTemplate = '<tr style="background:#ddd;cursor:pointer;" attribute1="{0}" attribute2="{1}"><td>{2}</td><td>{3}</td><td>{4}</td><td>{5}</td><td>{6}</td><td>{7}</td></tr>';

    rowTemplate.format(attribute1, attribute2,cell1,cell2,cell3,cell4,cell5,cell6);

{{% /highlight %}}

Complete example

HTML table 

{{% highlight html %}}
<table>
    <tbody id="mytableBody">
        <tr>
            <td></td>
        </tr>
    </tbody>
</table>
{{% /highlight %}}

JavaScript

{{% highlight javascript %}}
	String.prototype.format = function() {
	  var s = this.toString();
	  for (var i = 0; i < arguments.length; i++) {       
	    var reg = new RegExp("\\{" + i + "\\}", "gm");             
	    s = s.replace(reg, arguments[i]);
	  }

	  return s;
	}

   var table = $("#mytableBody");
    var rowTemplate = '<tr style="background:#ddd;cursor:pointer;" attribute1="{0}" attribute2="{1}"><td>{2}</td><td>{3}</td><td>{4}</td><td>{5}</td><td>{6}</td><td>{7}</td></tr>';

    table.append(rowTemplate.format(attribute1, attribute2,cell1,cell2,cell3,cell4,cell5,cell6));

{{% /highlight %}}


A clean solution for a common problem that seems to have a million different methods to accomplish. Hope this solution works for you please comment if you have any suggestions on making it better.