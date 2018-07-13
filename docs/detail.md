## Detailed API Specification

Simplified Station Information API is called at input form of station name in the tutorial application([A Toy App](/docs/app.md)).

Open the following URL in the browser.

```
https://api.ekispert.jp/v1/json/station/light?name=渋谷&type=train&key=LE_EeMdKVHwJQSen
```

{% hint %}
You can use some useful Web browser's extensions to make JSON easy on the eyes.  
Note: [Extentions](/docs/extension.md)

![img](/img/10.png)

<p class="caption">Without extension</p>

![img](/img/use_extension.png)

<p class="caption">With extension</p>

{% endhint %}



|Parameters|Description|
|---|---|
|name|Station name (only Japanese)[^1].|
|type|Station's transportation type.|

![img](/img/station2.png)

<p class="caption">Detail of response</p>

## Footnote
[^1]: You can use other languages with an option in Standard plan. https://ekiworld.net/service/sier/webservice/index.html
