# Grader On Browser

The accompanied tool: a web that provides autograders to exercises.
  * The grading is done on the client side (on a browser)

## Js to get a remote file
  * The autograder may be standardized (probably as the one used for autolab), but with a js wrapper.
  * The reference answers may be stored as static files in a server.

```
function getText(){
    // read text from URL location
    var request = new XMLHttpRequest();
    request.open('GET', 'http://www.puzzlers.org/pub/wordlists/pocket.txt', true);
    request.send(null);
    request.onreadystatechange = function () {
        if (request.readyState === 4 && request.status === 200) {
            var type = request.getResponseHeader('Content-Type');
            if (type.indexOf("text") !== 1) {
                return request.responseText;
            }
        }
    }
}
function populateTables(){
    
    var outer_text = getText();
    outer_text = outer_text.split('\n');    // you can adjust the manner of parsing the received file (regexp)
    
    var tableHP = document.getElementById("tHP");
// Create an empty <tr> element and add it to the 1st position of the table:
    var row = tableHP.insertRow(tableHP.rows.length);
// Insert new cells (<td> elements) at the 1st and 2nd position of the "new" <tr> element:
    var cell1 = row.insertCell(0);
    var cell2 = row.insertCell(1);

// Add some text to the new cells:
    cell1.innerHTML = outer_text[0];
    cell2.innerHTML = outer_text[1];
}
```

!!! This might not work, because JS prevents reading from other website, i.e., avoiding a risk of **cross site scripting**
