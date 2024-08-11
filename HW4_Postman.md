# Задание №4
> Аутентификация и авторизация

1. Импортировать коллекцию Postman с практической части вебинара в https://www.postman.com/
2. Создать Bearer token на Github по документации в Postman
3. Отправить запрос с полученным токеном и получить успешный ответ
4. Приложить скрин в ДЗ на платформу
5. Создать API Key в NASA по документации в Postman, повторить п.3-4

<details><summary> <i>см. collection.json (развернуть)</i> </summary>

```json

  {
  "info": {
    "_postman_id": "c3a87c41-d21b-4e8e-8dd6-11fe86206bb7",
    "name": "Authorization_methods",
    "description": "# 🔐 Get started here\n\nPostman supports a range of authorization mechanisms to enable you to communicate securely with APIs.\n\nThis template contains examples of different types of authorization that are ready to be modified to fit your use case.\n\n- **Basic Auth:** This simple authorization method uses a username and password combination to grant access to API resources. Postman offers a built-in Basic Auth helper that makes it easy to include the required credentials in your API requests.\n    \n\n- **OAuth 1.0 & OAuth 2.0:** Postman supports both versions of the OAuth protocol, which involve complex flows including obtaining request tokens, user authorization, and exchanging tokens for access tokens. Postman streamlines this process by handling server-side interactions, managing tokens, and offering pre-built authorization helpers.\n    \n\n- **Bearer Token:** Commonly used with OAuth 2.0, this method involves sending a token in the request header to authenticate with the API.\n    \n\n- **API Key:** Postman supports API Key authorization, which requires including a unique key in the request headers or as a query parameter.\n    \n\n- **Digest Auth:** This method employs a challenge-response mechanism to ensure secure communication with APIs.\n    \n\n- **Hawk Authentication:** Postman supports the Hawk authorization method, which utilizes time-based, one-time-use tokens for secure API access.\n    \n\n## 🔖 **How to use this template**\n\n**Step 1:** Select the request for your relevant authorization type.\n\n**Step 2:** Check out the documentation for the selected request to learn more about the type of authorization and how to use it.\n\n**Step 3:** Complete the relevant details for your selected authorization type.\n\n(Note: The correct data values will be determined by your API on the server side. If you're using a third-party API, refer to the provider's documentation for more details about the required authorization type.)\n\n## ℹ️ Resources\n\n[Authorizing requests in Postman](https://learning.postman.com/docs/sending-requests/authorization/)",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json",
    "_exporter_id": "32243014"
  },
  "item": [
    {
      "name": "Basic Auth",
      "request": {
        "auth": {
          "type": "basic",
          "basic": [
            {
              "key": "username",
              "value": "example_username",
              "type": "string"
            },
            {
              "key": "password",
              "value": "example_password",
              "type": "string"
            },
            {
              "key": "saveHelperData",
              "type": "any"
            },
            {
              "key": "showPassword",
              "value": false,
              "type": "boolean"
            }
          ]
        },
        "method": "GET",
        "header": [],
        "url": {
          "raw": "https://httpbin.org/basic-auth/example_username/example_password",
          "protocol": "https",
          "host": [
            "httpbin",
            "org"
          ],
          "path": [
            "basic-auth",
            "example_username",
            "example_password"
          ]
        },
        "description": "This request uses Basic Auth to authenticate with an API.\n\n`httpbin.org` offers a Basic Auth demo endpoint, following the pattern `httpbin.org/basic-auth/{username}/{password}`. It then expects a Basic Auth header matching the `{username}` and `{password}` values to be included in the Request.\n\nTo see an authentication failure, head to the request's Authorization tab and try changing the username or password before sending the request again.\n\nTo use Basic Auth with your own API, just replace the Request URL with your endpoint. Head to the Authorization tab, enter the expected username and password for your API, and try sending the request again."
      },
      "response": []
    },
    {
      "name": "Github Bearer token",
      "request": {
        "auth": {
          "type": "bearer",
          "bearer": [
            {
              "key": "token",
              "value": "",
              "type": "string"
            }
          ]
        },
        "method": "POST",
        "header": [],
        "body": {
          "mode": "raw",
          "raw": "{\n    \"name\": \"Created with Postman\",\n    \"private\": true\n}",
          "options": {
            "raw": {
              "language": "json"
            }
          }
        },
        "url": {
          "raw": "https://api.github.com/user/repos",
          "protocol": "https",
          "host": [
            "api",
            "github",
            "com"
          ],
          "path": [
            "user",
            "repos"
          ]
        },
        "description": "This request uses a Personal Access Token as a Bearer Token to authenticate with the GitHub API and create a new private repository.\n\nTo start, you'll need to follow the [steps to generate a Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) on GitHub. You can generate a **classic token with 'repo' scope** to use with this request.\n\nOnce your token is generated, you must copy it immediately as it won't be shown again. Then go to this collection's \"variables\" tab and paste it as the current value for the `githubAccessToken` variable.\n\nView the Authorization tab for this request. Note it uses the 'Bearer token' auth method, and the value is pre-filled to reference the `githubAccessToken` variable we've set our Personal Access Token in.\n\nIf you want, adjust the name of the repository to be created in the 'Body' tab. Then hit 'Send' to create a new repository using Bearer token authentication."
      },
      "response": []
    },
    {
      "name": "API Key",
      "request": {
        "auth": {
          "type": "apikey",
          "apikey": [
            {
              "key": "value",
              "value": "",
              "type": "string"
            },
            {
              "key": "in",
              "value": "query",
              "type": "string"
            },
            {
              "key": "key",
              "value": "api_key",
              "type": "string"
            }
          ]
        },
        "method": "GET",
        "header": [],
        "url": {
          "raw": "https://api.nasa.gov/planetary/apod",
          "protocol": "https",
          "host": [
            "api",
            "nasa",
            "gov"
          ],
          "path": [
            "planetary",
            "apod"
          ]
        },
        "description": "This request uses API Key authentication. The \"API Key\" Postman Authorization option is used to set the key and value to be included as a query parameter. These can also be included as a header for APIs expecting the key there.\n\nTo get started, visit [https://api.nasa.gov/](https://api.nasa.gov/) to get an API key. Set the `nasaApiKey` collection variable to the key you are given."
      },
      "response": []
    },
    {
      "name": "Generate signed JWT",
      "event": [
        {
          "listen": "prerequest",
          "script": {
            "type": "text/javascript",
            "exec": [
              "// JWT generation script adapted from",
              "// https://gist.github.com/corbanb/db03150abbe899285d6a86cc480f674d",
              "",
              "var jwtSecret = pm.collectionVariables.get('jwtSecret') || ''",
              "",
              "// Set headers for JWT",
              "var header = {",
              "\t'typ': 'JWT',",
              "\t'alg': 'HS256'",
              "};",
              "",
              "// Prepare timestamp in seconds",
              "var currentTimestamp = Math.floor(Date.now() / 1000)",
              "",
              "var data = {",
              "    // include any additional data for the JWT payload here",
              "    // you may add registered claims like `iss` (issuer), `sub` (subject)",
              "    // or other public/private claims",
              "    // see https://jwt.io/introduction for more information on the content of JWTs",
              "\t'iat': currentTimestamp,",
              "\t'exp': currentTimestamp + 30, // expiry time is 30 seconds from time of creation",
              "}",
              "",
              "",
              "function base64url(source) {",
              "    // Encode in classical base64",
              "    encodedSource = CryptoJS.enc.Base64.stringify(source)",
              "    ",
              "    // Remove padding equal characters",
              "    encodedSource = encodedSource.replace(/=+$/, '')",
              "    ",
              "    // Replace characters according to base64url specifications",
              "    encodedSource = encodedSource.replace(/\\+/g, '-')",
              "    encodedSource = encodedSource.replace(/\\//g, '_')",
              "    ",
              "    return encodedSource",
              "}",
              "",
              "// encode header",
              "var stringifiedHeader = CryptoJS.enc.Utf8.parse(JSON.stringify(header))",
              "var encodedHeader = base64url(stringifiedHeader)",
              "",
              "// encode data",
              "var stringifiedData = CryptoJS.enc.Utf8.parse(JSON.stringify(data))",
              "var encodedData = base64url(stringifiedData)",
              "",
              "// build token",
              "var token = `${encodedHeader}.${encodedData}`",
              "",
              "// sign token",
              "var signature = CryptoJS.HmacSHA256(token, jwtSecret)",
              "signature = base64url(signature)",
              "var signedToken = `${token}.${signature}`",
              "",
              "pm.variables.set('jwtSigned', signedToken)",
              "console.log('Signed and encoded JWT', signedToken)",
              ""
            ]
          }
        }
      ],
      "request": {
        "auth": {
          "type": "bearer",
          "bearer": [
            {
              "key": "token",
              "value": "{{jwtSigned}}",
              "type": "string"
            }
          ]
        },
        "method": "POST",
        "header": [],
        "url": {
          "raw": "https://postman-echo.com/post",
          "protocol": "https",
          "host": [
            "postman-echo",
            "com"
          ],
          "path": [
            "post"
          ]
        },
        "description": "This request uses a pre-request script to generate, encode, and sign a JWT (JSON Web Token). This token is sent as a Bearer token authorization header.\n\nThis allows sending requests to a JWT-authenticated API you own or have the signing secret for without manually generating tokens eg. through an auth flow.\n\nSet the `jwtSecret` collection variable's current value to your signing secret to get started.\n\nYou can also modify the Pre-request Script to include additional data in the JWT payload, such as `iss` (issuer) or `sub` (subject) fields."
      },
      "response": []
    },
    {
      "name": "Google OAuth 2.0",
      "request": {
        "auth": {
          "type": "oauth2",
          "oauth2": [
            {
              "key": "clientSecret",
              "value": "{{googleClientSecret}}",
              "type": "string"
            },
            {
              "key": "clientId",
              "value": "{{googleClientId}}",
              "type": "string"
            },
            {
              "key": "grant_type",
              "value": "authorization_code",
              "type": "string"
            },
            {
              "key": "authUrl",
              "value": "https://accounts.google.com/o/oauth2/v2/auth",
              "type": "string"
            },
            {
              "key": "scope",
              "value": "https://www.googleapis.com/auth/userinfo.email https://www.googleapis.com/auth/userinfo.profile https://www.googleapis.com/auth/spreadsheets.readonly https://www.googleapis.com/auth/spreadsheets https://www.googleapis.com/auth/drive.file https://spreadsheets.google.com/feeds/",
              "type": "string"
            },
            {
              "key": "accessTokenUrl",
              "value": "https://oauth2.googleapis.com/token",
              "type": "string"
            },
            {
              "key": "tokenName",
              "value": "Google Sheets",
              "type": "string"
            },
            {
              "key": "useBrowser",
              "value": true,
              "type": "boolean"
            },
            {
              "key": "addTokenTo",
              "value": "header",
              "type": "string"
            },
            {
              "key": "accessToken",
              "type": "any"
            },
            {
              "key": "callBackUrl",
              "type": "any"
            },
            {
              "key": "clientAuth",
              "type": "any"
            },
            {
              "key": "grantType",
              "type": "any"
            },
            {
              "key": "username",
              "type": "any"
            },
            {
              "key": "password",
              "type": "any"
            },
            {
              "key": "tokenType",
              "type": "any"
            },
            {
              "key": "redirectUri",
              "type": "any"
            },
            {
              "key": "refreshToken",
              "type": "any"
            }
          ]
        },
        "method": "GET",
        "header": [],
        "url": {
          "raw": "https://sheets.googleapis.com/v4/spreadsheets/{{googleSheetId}}",
          "protocol": "https",
          "host": [
            "sheets",
            "googleapis",
            "com"
          ],
          "path": [
            "v4",
            "spreadsheets",
            "{{googleSheetId}}"
          ]
        },
        "description": "This request is ready to access a Google Sheet document via the Google Sheets API, authenticating with Google via interactive OAuth 2.0.\n\nIt requires three Collection Variables to be filled:\n\n- `googleClientId` - a Google API client ID\n- `googleClientSecret` - a Google API client secret\n- `googleSheetId` - ID of the Google Sheet to fetch\n    \n\nOnce you've populated these Collection Variables, just hit \"Get New Access Token\" in the Request Authorization tab to start the interactive OAuth 2.0 flow. Postman will remember the token returned, and use it when you send the Request to fetch a Sheet."
      },
      "response": []
    }
  ],
  "event": [
    {
      "listen": "prerequest",
      "script": {
        "type": "text/javascript",
        "exec": [
          ""
        ]
      }
    },
    {
      "listen": "test",
      "script": {
        "type": "text/javascript",
        "exec": [
          ""
        ]
      }
    }
  ],
  "variable": [
    {
      "key": "googleSheetId",
      "value": "1K927eIP2LFCoGf7hRhhUmmOtNi-sA1C90nnm6h4-s4g",
      "type": "string"
    },
    {
      "key": "googleClientId",
      "value": "665788081455-egofcjku4toffv0jpa4iciqlgku7t94f.apps.googleusercontent.com",
      "type": "string"
    },
    {
      "key": "googleClientSecret",
      "value": "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",
      "type": "string"
    },
    {
      "key": "githubAccessToken",
      "value": "Github Personal Access Token",
      "type": "string"
    },
    {
      "key": "jwtSecret",
      "value": "JWT signing secret",
      "type": "string"
    },
    {
      "key": "nasaApiKey",
      "value": "NASA API Key",
      "type": "string"
    },
    {
      "key": "hawkId",
      "value": "dh37fgj492je",
      "type": "string"
    },
    {
      "key": "hawkKey",
      "value": "werxhqb98rpaxn39848xrunpaw3489ruxnpa98w4rxn",
      "type": "string"
    },
    {
      "key": "digestUsername",
      "value": "postman",
      "type": "string"
    },
    {
      "key": "digestPassword",
      "value": "password",
      "type": "string"
    },
    {
      "key": "oauth1Key",
      "value": "RKCGzna7bv9YD57c",
      "type": "string"
    },
    {
      "key": "oauth1Secret",
      "value": "D+EdQ-gs$-%@2Nu7",
      "type": "string"
    }
  ]
}

```
</details>

-------------------


<table width="1000" border="1">
<thead>
  <tr>
    <td rowspan="3"><img width="300px" src="https://github.com/user-attachments/assets/9d985eaa-c3fc-4ab3-b84c-4acbd7c1bbb2"></td>
    <td colspan="2" width="700"><p align="center"><b> Postman</b></p></td>
  </tr>
  <tr>
    <td>Дата</td>
    <td>11.08.2024</td>
  </tr>
  <tr>
    <td>Версия</td>
    <td>1.0</td>
  </tr>
</thead>
</table>
