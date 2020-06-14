---
description: >-
  Convert HTML to an image (png, jpg or webp) with C# + the HTML/CSS to Image
  API. Renders exactly like Google Chrome.
---

# C\#

In this post, you'll learn how to convert HTML into an image using C\#.

### Example Code

This example uses the HTML/CSS to Image API to create an image. It handles the authentication for you, as well as POSTing the html/css to the API.

The response is `JSON` with the URL to the generated image.

```csharp
using System.Net;
namespace htciExample
{
    class Program
    {
        static void Main()
        {
            byte[] result;
            string html = "<div class='ping'>Pong ✅</div>";
            string css = ".ping {padding: 20px; font-family:'sans-serif'; }";
            using (var client = new WebClient())
            {
                string credentials = Convert.ToBase64String(Encoding.ASCII.GetBytes("user_id:api_key"));
                client.Headers[HttpRequestHeader.Authorization] = "Basic " + credentials;

                result = client.UploadValues(
                    "https://hcti.io/v1/image",
                    "POST", 
                    new System.Collections.Specialized.NameValueCollection()
                    {
                        { "html", html }, { "css", css }
                    }
                    );
            }
            string resultString = System.Text.Encoding.UTF8.GetString(result);
            Console.WriteLine(resultString);
            '{"url":"https://hcti.io/v1/image/404ed70d-dcb9-4778-9be4-fad912321d5b"}
        }
    }
}
```

## More examples <a id="more-examples"></a>

This was a simple example. To see a full list of available parameters, take a look at [Creating an image](../getting-started/creating-an-image.md).

