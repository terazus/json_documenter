

We want to generate documentation of our JSON-schemas using Sphinx and hosting the resulting output on github.

### INSTALL

- Sphinx:
<pre>
apt-get install python-sphinx
</pre>

- Navigate to the directory you want to create the documentation in and generate all the files with:
<pre>
sphinx-quickstart
</pre>

- Install sphinx-git:
<pre>
pip install sphinx-git
</pre>


### GENERATE THE DOCS

- Open the config.py file generated by sphinx and add the extension:
<pre>
extensions = ['sphinx_git']
</pre>

- Generate the Sphinx HTML:
<pre>
make html
</pre>


### EDIT THE CODE

Clone the code:
<pre>
git clone https://github.com/terazus/json_documenter.git
</pre>

Open the HTML file you want to edit (html/dats.html for dats) with a text editor and do the following:

- Under the ```<!DOCTYPE html>``` declaration modify
```<html class="no-js lt-ie9" lang="en">```
        to
         <html class="no-js lt-ie9" lang="en" ng-app="generatorApp">
        
        and
        <html class="no-js" lang="en">
        to

        <html class="no-js" lang="en" ng-app="generatorApp">```


- In the ```<HEAD>``` tag add those tags:

        <script src="json_documenter/lib/angular.min.js"\></script\>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.6.5/angular-route.min.js"></script>
        <script src="json_documenter/myapp.js"></script>
        <link rel="stylesheet" href="json_documenter/app.css" type="text/css" />


- Change tag:

         <body class="wy-body-for-nav">
to
         <body class="wy-body-for-nav" ng-controller="documenterController as documenter">

- Search the HTML list that controls the left menu. Add to it (under the proper item) the following code:

        <ul>
            <li ng-repeat="(key, item) in documenter.loaded_specs">
                <a class="reference internal" ng-href="#{{key|removeExtraStr}}" target="_self">{{item.title}}</a>
            </li>
        </ul>


- Change the main html at your convenience and add
        <div schema-loader="documenter.main_spec" parent-key="''">
        </div>

        <div ng-repeat="(key, item) in documenter.loaded_specs"
             schema-loader="documenter.loaded_specs[key]"
             parent-key="key"
             class="col-lg-12 col-sm-12 col-md-12 schema">
        </div>
wherever you want to add the doc.

- Open index.html in your navigator and verify the output.

- Remove the .git repo in the json_documenter/ directory, publish to github and enable web hosting.
