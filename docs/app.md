# A toy App

Let's implement an application with Ekispert Web Service.

![img](/img/1.png)

<p class="caption">Example</p>

Ekispert Web Service has two plans: Free plan which is offered for free and Standard plan that all features are available.

This tutorial uses only features provided in Free plan.

You can use access key for tutorial: **LE_EeMdKVHwJQSen**  
Note: This key is only for trial.

Step 1, make following HTML code(List 1).

▼List 1. HTML code

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>Ekispert Web Service Tutorial</title>
  <script src="https://cdn.rawgit.com/EkispertWebService/GUI/84587/expGuiStation/expGuiStation.js"></script>
  <script src="https://cdn.rawgit.com/EkispertWebService/GUI/84587/expGuiCourseLight/expGuiCourseLight.js"></script>
  <link rel="stylesheet" href="https://cdn.rawgit.com/EkispertWebService/GUI/84587/expGuiStation/expCss/expGuiStation.css" />
</head>
<script>
var accessKey = "LE_EeMdKVHwJQSen";
var depStationApp;
var arrStationApp;
var courseLight;

function init() {
  depStationApp = new expGuiStation(document.getElementById("depStation"));
  depStationApp.setConfigure("key", accessKey);
  depStationApp.setConfigure("ssl", true);
  depStationApp.dispStation();

  arrStationApp = new expGuiStation(document.getElementById("arrStation"));
  arrStationApp.setConfigure("key", accessKey);
  arrStationApp.setConfigure("ssl", true);
  arrStationApp.dispStation();

  courseLight = new expGuiCourseLight();
  courseLight.setConfigure("key", accessKey);
  courseLight.setConfigure("ssl", true);
}

window.onload = function() {
  var search = document.getElementById('search');
  search.addEventListener('click', (e) => {

    depStationApp.closeStationList();
    arrStationApp.closeStationList();

    var searchObj = courseLight.createSearchInterface();

    searchObj.setFrom(depStationApp.getStationCode());
    searchObj.setTo(arrStationApp.getStationCode());

    courseLight.search(searchObj, function(isSuccess) {
      if (!isSuccess) {
        alert("Could not get result.");
      } else {
        document.getElementById("ekispertUrl").textContent = "Get \"Ekispert for web\" result.";
        document.getElementById("ekispertUrl").href = courseLight.getResourceURI();
      }
    });
  })
};

window.addEventListener('load', init);

</script>
<body>
<div>
  Departure
  <div id="depStation"></div>
</div>
<div>
  Arrival
  <div id="arrStation"></div>
</div>
<button id="search">Search</button>
<a id="ekispertUrl" href="" target="_blank"></a>
</body>
</html>
```

In this example, some external file links for HTML5 Interface Sample[^3] are included such as `<script src="https://cdn.rawgit.com/EkispertWebService/GUI/84587/expGuiStation/expGuiStation.js"></script>`.

Note: HTML5 Interface Sample is a sample implemented by HTML, JavaScript and CSS.

Now your application enables to search stations and routes.

![img](/img/result.png)

<p class="caption">Execute an application</p>

{% hint %}
If it doesn't work successfully, you can debug by Web browser's DevTools.  
Note: [DevTools](/docs/devtool.md)
{% endhint %}


## Footnote
[^1]: Ekispert Web Service Free plan https://ekiworld.net/service/lp/webservice/
[^2]: Ekispert Web Service Standard plan https://ekiworld.net/service/sier/webservice/index.html
[^3]: HTML5 Interface Sample https://github.com/EkispertWebService/GUI
