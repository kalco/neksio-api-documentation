**API Documentation:**

---

# Product API Documentation

Welcome to the Product API documentation. This API allows you to retrieve an authentication token and fetch a list of products.

**Base URL:** `https://g1.store.neksio.mk/api`

## Authentication

Before accessing the products, you need to obtain an access token by sending a POST request to the `/GetToken` endpoint.

### Request

**Endpoint:** `/GetToken`

#### Request Body

| Field      | Type   | Description               |
|------------|--------|---------------------------|
| `email`    | string | Your email address       |
| `password` | string | Your password            |

### Response

A successful response will include the access token required for further API calls.

#### Response Example

```json
{
    "name": "SOFTWARE MICROSOFT OFFICE PROFESSIONAL PLUS 2021  SKU-T5D-03280",
    "description": "<div class=\"feature_UbV5SNP5Eo\"><div class=\"feature_UbV5SNP5Eo\"><div class=\"featureHeader_UbV5SNP5Eo\"><div class=\"text_TAw0W35QK_ comfy_TAw0W35QK_ sizeTitle2_TAw0W35QK_ weightNormal_TAw0W35QK_ primary_i3MsQsqoe0\">Key Benefits</div></div><div><div class=\"\"><div class=\"descriptionAsTitle_UbV5SNP5Eo\"><div class=\"js-injected-html text_UbV5SNP5Eo\">One-time purchase for 1 PC or Mac</div></div></div></div><div><div class=\"feature_UbV5SNP5Eo\"><div class=\"descriptionAsTitle_UbV5SNP5Eo\"><div class=\"js-injected-html text_UbV5SNP5Eo\">Classic 2021 versions of Word, Excel, PowerPoint, and Outlook</div></div></div></div><div><div class=\"feature_UbV5SNP5Eo\"><div class=\"descriptionAsTitle_UbV5SNP5Eo\"><div class=\"js-injected-html text_UbV5SNP5Eo\">Microsoft support included for first 60 days at no extra cost</div></div></div></div><div><div class=\"feature_UbV5SNP5Eo\"><div class=\"descriptionAsTitle_UbV5SNP5Eo\"><div class=\"js-injected-html text_UbV5SNP5Eo\">Compatible with Windows 11, Windows 10, and the three most recent versions of macOS</div></div></div></div><div><div class=\"feature_UbV5SNP5Eo\"><div class=\"descriptionAsTitle_UbV5SNP5Eo\"><div class=\"js-injected-html text_UbV5SNP5Eo\">Works with Microsoft Teams</div></div></div></div><div><div class=\"feature_UbV5SNP5Eo\"><div class=\"featureHeader_UbV5SNP5Eo\"><div class=\"text_TAw0W35QK_ comfy_TAw0W35QK_ sizeTitle3_TAw0W35QK_ weightNormal_TAw0W35QK_ primary_i3MsQsqoe0\">Office Home &amp; Business 2021</div></div><div><div class=\"js-injected-html text_UbV5SNP5Eo\">The essentials to get it all done. Office Home &amp; Business 2021 is for families and small businesses who want classic Office apps and email. It includes Word, Excel, PowerPoint, and Outlook for Windows 11, Windows 10 and macOS. A one-time purchase installed on 1 PC or Mac for use at home or work.</div></div></div>",
    "productCode": "01095",
    "barCode": "889842098570",
    "category": "СОФТВЕР",
    "subCategory": null,
    "b2BPriceWTax": 16000,
    "b2BPriceWOTax": 13559.32,
    "retailPriceWTax": 16000,
    "retailPriceWOTax": 13559.32,
    "tax": 18,
    "inStock": true,
    "manufacturer": null,
    "guaranteePeriodInDays": 0,
    "coverImage": "https://g1.store.neksio.mk/images/products/product_10531_0.png",
    "galleryImages": []
  },
```

## Products

Once you have obtained the access token, you can use it to fetch the list of products.

### Request

**Endpoint:** `/GetProducts`

#### Headers

Include the access token obtained from the authentication step.

| Header         | Value                        |
|----------------|------------------------------|
| `Authorization`| `Bearer your-access-token`   |

### Response

A successful response will include a list of products.

#### Response Example

```json
[
  {
    "id": 1,
    "name": "Product A"
  },
  {
    "id": 2,
    "name": "Product B"
  }
]
```

---

In this documentation, we've provided details for both the authentication process and the products retrieval process. The documentation includes information on endpoints, request methods, request parameters, request headers, response formats, and response examples.

Remember to replace placeholders like `your-access-token` with actual values when implementing and using the API. Also, adapt the documentation to your specific API structure and requirements.

### Examples of integration

**PHP Integration Example:**

```php
<?php
// Fetch Token
$tokenUrl = 'https://g1.store.neksio.mk/api/Product/GetToken';
$tokenData = json_encode(array(
    'email' => 'myemail@com.com',
    'password' => 'Password'
));
$tokenHeaders = array(
    'Content-Type: application/json',
    'Accept: */*'
);

$tokenCurl = curl_init($tokenUrl);
curl_setopt($tokenCurl, CURLOPT_RETURNTRANSFER, true);
curl_setopt($tokenCurl, CURLOPT_HTTPHEADER, $tokenHeaders);
curl_setopt($tokenCurl, CURLOPT_POST, true);
curl_setopt($tokenCurl, CURLOPT_POSTFIELDS, $tokenData);

$tokenResponse = curl_exec($tokenCurl);
$tokenInfo = curl_getinfo($tokenCurl);

curl_close($tokenCurl);

if ($tokenInfo['http_code'] === 200) {
    $accessToken = json_decode($tokenResponse, true)['token'];

    // Use the token to fetch products
    $productsUrl = 'https://g1.store.neksio.mk/api/Product/GetProducts';
    $productsHeaders = array(
        'Authorization: Bearer ' . $accessToken,
        'Accept: */*'
    );

    $productsCurl = curl_init($productsUrl);
    curl_setopt($productsCurl, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($productsCurl, CURLOPT_HTTPHEADER, $productsHeaders);

    $productsResponse = curl_exec($productsCurl);
    $productsInfo = curl_getinfo($productsCurl);

    curl_close($productsCurl);

    if ($productsInfo['http_code'] === 200) {
        $products = json_decode($productsResponse, true);
        print_r($products); // Display the fetched products
    } else {
        echo 'Error fetching products.';
    }
} else {
    echo 'Error fetching token.';
}
?>
```

---

**Python Integration Example:**

```python
import requests

# Fetch Token
token_url = 'https://g1.store.neksio.mk/api/Product/GetToken'
token_data = {
    'email': 'myemail@com.com',
    'password': 'Password'
}
token_headers = {
    'Content-Type': 'application/json',
    'Accept': '*/*'
}

token_response = requests.post(token_url, json=token_data, headers=token_headers)
if token_response.status_code == 200:
    access_token = token_response.json()['token']

    # Use the token to fetch products
    products_url = 'https://g1.store.neksio.mk/api/Product/GetProducts'
    products_headers = {
        'Authorization': f'Bearer {access_token}',
        'Accept': '*/*'
    }

    products_response = requests.get(products_url, headers=products_headers)
    if products_response.status_code == 200:
        products = products_response.json()
        print(products)  # Print the fetched products
    else:
        print('Error fetching products.')
else:
    print('Error fetching token.')

```
---
**React Integration Example:**

_Assuming you're using functional components and hooks:_

```javascript
import React, { useState, useEffect } from 'react';
import axios from 'axios';

function App() {
  const [token, setToken] = useState('');
  const [products, setProducts] = useState([]);

  useEffect(() => {
    // Fetch token
    axios.post('https://g1.store.neksio.mk/api/Product/GetToken', {
      email: 'myemail@com.com',
      password: 'Password'
    })
    .then(response => {
      const accessToken = response.data.token;
      setToken(accessToken);

      // Use the token to fetch products
      axios.get('https://g1.store.neksio.mk/api/Product/GetProducts', {
        headers: {
          Authorization: `Bearer ${accessToken}`
        }
      })
      .then(productsResponse => {
        setProducts(productsResponse.data);
      })
      .catch(error => {
        console.error('Error fetching products:', error);
      });
    })
    .catch(error => {
      console.error('Error fetching token:', error);
    });
  }, []);

  return (
    <div className="App">
      <h1>Products</h1>
      <ul>
        {products.map(product => (
          <li key={product.id}>{product.name}</li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```
---
**Java Integration Example:**

Here's an example of using the `java.net` package in Java to integrate with the API endpoints. Please note that this is a basic example and you might want to handle exceptions and errors more thoroughly in a production environment.

```java
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Scanner;

public class APIClient {
    public static void main(String[] args) throws IOException {
        // Fetch Token
        String tokenUrl = "https://g1.store.neksio.mk/api/Product/GetToken";
        String tokenData = "{\"email\": \"myemail@com.com\", \"password\": \"Password\"}";

        URL tokenApiUrl = new URL(tokenUrl);
        HttpURLConnection tokenConnection = (HttpURLConnection) tokenApiUrl.openConnection();
        tokenConnection.setRequestMethod("POST");
        tokenConnection.setRequestProperty("Content-Type", "application/json");
        tokenConnection.setRequestProperty("Accept", "*/*");
        tokenConnection.setDoOutput(true);

        try (OutputStream os = tokenConnection.getOutputStream()) {
            byte[] input = tokenData.getBytes("utf-8");
            os.write(input, 0, input.length);
        }

        try (InputStream responseStream = tokenConnection.getInputStream()) {
            String tokenResponse = new Scanner(responseStream, "utf-8").useDelimiter("\\A").next();
            String accessToken = tokenResponse.contains("token") ? tokenResponse.split("\"token\":\"")[1].split("\"")[0] : null;

            if (accessToken != null) {
                // Use the token to fetch products
                String productsUrl = "https://g1.store.neksio.mk/api/Product/GetProducts";
                URL productsApiUrl = new URL(productsUrl);
                HttpURLConnection productsConnection = (HttpURLConnection) productsApiUrl.openConnection();
                productsConnection.setRequestMethod("GET");
                productsConnection.setRequestProperty("Authorization", "Bearer " + accessToken);
                productsConnection.setRequestProperty("Accept", "*/*");

                try (InputStream productsResponseStream = productsConnection.getInputStream()) {
                    String productsResponse = new Scanner(productsResponseStream, "utf-8").useDelimiter("\\A").next();
                    System.out.println(productsResponse);
                }
            }
        }
    }
}
```
---
Please note that the examples provided are basic and do not include extensive error handling. In real-world scenarios, you should handle exceptions, errors, and edge cases more thoroughly.

