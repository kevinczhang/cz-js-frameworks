---
description: AJAX = Asynchronous JavaScript And XML
---

# AJAX

AJAX just uses a combination of:

* A browser built-in `XMLHttpRequest` object \(to request data from a web server\)
* JavaScript and HTML DOM \(to display or use the data\)

```javascript
function loadDoc() {
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
     document.getElementById("demo").innerHTML = this.responseText;
    }
  };
  xhttp.open("GET", "ajax_info.txt", true);
  xhttp.send();
}
```

