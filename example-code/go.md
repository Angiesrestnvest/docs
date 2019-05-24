---
description: Converting HTML/CSS to an Image with Go
---

# Go

This code only uses the standard library, so the only prerequisite is that you have go installed.

#### Example code

This code sample creates our request body, formats it, creates a new POST request, sets our authentication, creates a client, performs the POST to the API, reads the response and then prints it out the response as a string. The response will be json with the URL to the generated image.

{% code-tabs %}
{% code-tabs-item title="main.go" %}
```go
package main
import (
    "bytes"
    "encoding/json"
    "fmt"
    "io/ioutil"
    "log"
    "net/http"
    "time"
)
const (
    userID = "your_user_id"
    apiKey = "your_api_key"
)
func main() {
    data := map[string]string{
        "html": "<div class='ping'>Pong ✅</div>",
        "css":  ".ping { padding: 20px; font-family: 'sans-serif'; }",
    }
    reqBody, err := json.Marshal(data)
    if err != nil {
        log.Fatalf("unable to marshal data: %s", err.Error())
    }
    req, err := http.NewRequest("POST", "https://hcti.io/v1/image", bytes.NewReader(reqBody))
    if err != nil {
        log.Fatalf("unable to create new request: %s", err.Error())
    }
    req.SetBasicAuth(userID, apiKey)
    client := &http.Client{Timeout: time.Second * 10}
    resp, err := client.Do(req)
    if err != nil {
        log.Fatalf("request was unsuccessful: %s", err.Error())
    }
    defer resp.Body.Close()
    body, err := ioutil.ReadAll(resp.Body)
    if err != nil {
        log.Fatalf("unable to read response body: %s", err.Error())
    }
    fmt.Println(string(body))

    // {"url":"https://hcti.io/v1/image/f1e2762b-1f95-4f99-ab5d-0444b26dfd42"}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### More examples

For more advanced examples, [take a look here](../#examples).

