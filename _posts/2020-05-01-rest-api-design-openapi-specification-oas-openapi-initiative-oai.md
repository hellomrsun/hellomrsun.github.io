---
layout: post
# title: REST API Design - What is OpenAPI-compliant API?
# excerpt_separator:  <!--more-->
# tags: REST | Web-Api
# canonical_url: 'https://sunjiangong.com/rest-api-design-openapi-specification-oas-openapi-initiative-oai/'
read_time: true
show_date: true
title:  REST API Design - What is OpenAPI-compliant API?
date:   2020-05-01 08:00:00 +0100
description: REST API Design - What is OpenAPI-compliant API? Web API
img: posts/uncategorized/open-api.png
tags: [REST, WebApi]
author: SUN Jiangong
# github:  hellomrsun
mathjax: yes
---

The OpenAPI Initiative (**OAI**) was created in order to standardize the API design.The OpenAPI Specification (**OAS**) was originally based on the Swagger Specification, donated by SmartBear Software.

The OpenAPI is programming language agnostic. 

You can see the OpenAPI Specification change history [here](#openapi-specification-history) 	

<br/>

<!--more-->

# What should you do to implement a OAS compliant API?

<br/>

## 1. Use correct media types

Media type is the data type of API requests and responses.

Media type could be text, image, audio, or video etc.

The most common used media types are **JSON**, **XML** and **images**. 

Examples:

```
text/plain; charset=utf-8
application/json
application/xml
text/json
```

## 2. Use appropriate HTTP response status codes

There are 5 types of status codes as following:

```
1XX: informational status
2XX: successful status
3XX: redirection status
4XX: client error status
5XX: server error status
```

Remember to use the appropriate response statuses in your API.

Here are some common used status:
- 200 => OK
- 201 => Created
- 400 => Bad request
- 403 => Forbidden
- 404 => Not Found
- 500 => Server Internal Error
- 503 => Server Unavailable

See [full HTTP status list](#full-http-status-list)


## 3. Use OpenAPI Document type

The OpenAPI document should be in the format of JSON (.json) or YAML (.yaml).

It's recommended to name it as **openapi.json** or **openapi.yaml**.

For those who is not familiar with YAML (Yet Another Markup Language): YAML is a superset of JSON.

YAML is better for configuration, JSON is better for serialization.

YAML and JSON are convertible from one to another.

[Convert JSON to YAML](https://www.json2yaml.com/)

[Convert YAML to JSON](https://www.convertjson.com/yaml-to-json.htm)


## 4. Use standard data types

OpenAPI standard data types are:

| type    | format    |
| ------- | --------- |
| integer | int32     |
| integer | int64     |
| number  | float     |
| number  | double    |
| integer | int32     |
| string  | byte      |
| string  | binary    |
| string  | date      |
| string  | date-time |
| string  | password  |
| string  |           |
| boolean |           |


## 5. What is the OpenAPI Document structure

The Open API document may vary according to your project requirement.
It could be very simple or complex.

Here is an OpenAPI example implemented in C# and Swashbuckle.

![](./../../../assets/img/posts/2020-05-01-OpenApi/01_document_structure.PNG)

You can see the Open API version is 3.0.1.

### 5.1 info section (Open API Info)

You can find the API title, description, terms of server, contact name, url, email and license information in this part.

![](./../../../assets/img/posts/2020-05-01-OpenApi/02_open_api_info.PNG)

### 5.2 servers section (API servers)

You can find the API urls, ports, versions etc hosted on different servers.

![](./../../../assets/img/posts/2020-05-01-OpenApi/03_open_api_servers.PNG)

### 5.3 paths section (API routes/operations)

Here you can find all the operations available in the API.

- Create a grape with POST action:

The input is Grape model, and the format could be application/json, text/json, or application/*+json, the response status code could be 201 (grape created) or 500 (server error).

![](./../../../assets/img/posts/2020-05-01-OpenApi/04_open_api_paths_post.PNG)

- Get all grapes with GET action:

The response status could be 200 with a list of grapes or 500 with a server error.

![](./../../../assets/img/posts/2020-05-01-OpenApi/05_open_api_paths_get.PNG)

Delete a grape with id with DELETE action:

![](./../../../assets/img/posts/2020-05-01-OpenApi/06_open_api_paths_delete.PNG)


### 5.4 components

Components contain all the API request and response models.

There are 3 models involved: Grape, Link, and GrapeIEnumerableHateoasModel.

![](./../../../assets/img/posts/2020-05-01-OpenApi/07_open_api_components.PNG)

<br/>

We have seen a basic OpenAPI document, but it's not all.

You can explore more in the last OpenAPI Specification in the [references](#references).

<br/>

### OpenAPI Specification History:

| API version | Publication date | Details                                               |
| ----------- | ---------------- | ----------------------------------------------------- |
| 1.0         | **2011-08-10**   | **First release of the Swagger Specification**        |
| 1.1         | 2012-08-22       | Release of Swagger 1.1                                |
| 1.2         | 2014-03-14       | Initial release of the formal document.               |
| 2.0         | 2014-09-08       | Release of Swagger 2.0                                |
| 2.0         | **2015-12-31**   | **Donation of Swagger 2.0 to the OpenAPI Initiative** |
| 3.0.0-rc0   | 2017-02-28       | Implementer’s Draft of the 3.0 specification          |
| 3.0.0       | **2017-07-26**   | **Release of the OpenAPI Specification 3.0.0**        |
| 3.0.1       | 2017-12-06       | Patch release of the OpenAPI Specification 3.0.1      |
| 3.0.2       | 2018-10-08       | Patch release of the OpenAPI Specification 3.0.2      |
| 3.0.3       | 2020-02-20       | Patch release of the OpenAPI Specification 3.0.3      |

<br/>

### Full HTTP status list:

| Code    | Status                        |
| ------- | ----------------------------- |
| **1XX** | **Information**               |
| 100     | Continue                      |
| 101     | Switching Protocols           |
| **2XX** | **Successful**                |
| 200     | OK                            |
| 201     | Created                       |
| 202     | Accepted                      |
| 203     | Non-Authoritative Information |
| 204     | No Content                    |
| 205     | Reset Content                 |
| 206     | Partial Content               |
| **3XX** | **Redirection**               |
| 300     | Multiple Choices              |
| 301     | Moved Permanently             |
| 302     | Found                         |
| 303     | See Other                     |
| 304     | Not Modified                  |
| 305     | Use Proxy                     |
| 307     | Temporary Redirect            |
| **4XX** | **Client error**              |
| 400     | Bad Request                   |
| 401     | Unauthorized                  |
| 402     | Payment Required              |
| 403     | Forbidden                     |
| 404     | Not Found                     |
| 405     | Method Not Allowed            |
| 406     | Not Acceptable                |
| 407     | Proxy Authentication Required |
| 408     | Request Timeout               |
| 409     | Conflict                      |
| 410     | Gone                          |
| 411     | Length Required               |
| 412     | Precondition Failed           |
| 413     | Payload Too Large             |
| 414     | URI Too Long                  |
| 415     | Unsupported Media Type        |
| 416     | Range Not Satisfiable         |
| 417     | Expectation Failed            |
| 426     | Upgrade Required              |
| **5XX** | **Server error**              |
| 500     | Internal Server Error         |
| 501     | Not Implemented               |
| 502     | Bad Gateway                   |
| 503     | Service Unavailable           |
| 504     | Gateway Timeout               |
| 505     | HTTP Version Not Supported    |

<br/>

### Complete OpenAPI document

```json
{
  "openapi": "3.0.1",
  "info": {
    "title": "SignalR .NET core API",
    "description": "A SignalR .NET core API Demo",
    "termsOfService": "http://www.sunjiangong.com/terms",
    "contact": {
      "name": "Mr SUN Jiangong",
      "url": "http://www.sunjiangong.com/",
      "email": "contact@sunjiangong.com"
    },
    "license": {
      "name": "Apache License 2.0",
      "url": "https://www.apache.org/licenses/LICENSE-2.0.html"
    },
    "version": "1.1.0"
  },
  "servers": [
    {
      "url": "http://localhost:1234",
      "description": "DEV server",
      "variables": {
        "BasePath": {
          "default": "v1"
        },
        "UserName": {
          "default": "Jiangong",
          "description": "Demo User"
        },
        "Port": {
          "default": "1234",
          "description": "Port number",
          "enum": [
            "1234",
            "1235"
          ]
        }
      }
    },
    {
      "url": "http://localhost:5678",
      "description": "INT server",
      "variables": {
        "BasePath": {
          "default": "v2"
        },
        "UserName": {
          "default": "Jiangong",
          "description": "Demo User"
        },
        "Port": {
          "default": "5678",
          "description": "Port number",
          "enum": [
            "5678",
            "5679"
          ]
        }
      }
    }
  ],
  "paths": {
    "/api/v1/grapes": {
      "post": {
        "tags": [
          "Grapes"
        ],
        "summary": "Create a new grape",
        "requestBody": {
          "description": "Grape",
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/Grape"
              }
            },
            "text/json": {
              "schema": {
                "$ref": "#/components/schemas/Grape"
              }
            },
            "application/*+json": {
              "schema": {
                "$ref": "#/components/schemas/Grape"
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "Grape is created"
          },
          "500": {
            "description": "Internal Server Error"
          }
        }
      },
      "get": {
        "tags": [
          "Grapes"
        ],
        "summary": "Get all the grapes",
        "responses": {
          "200": {
            "description": "Returns a list of grapes",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Grape"
                  }
                }
              }
            }
          },
          "500": {
            "description": "Internal Server Error"
          }
        }
      }
    },
    "/api/v1/grapes/{id}": {
      "delete": {
        "tags": [
          "Grapes"
        ],
        "summary": "Delete a grape",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "description": "grape id",
            "required": true,
            "schema": {
              "type": "integer",
              "description": "grape id",
              "format": "int32"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Deletion is ok"
          },
          "500": {
            "description": "Internal Server Error"
          }
        }
      }
    },
    "/api/v1/hateoas-grapes": {
      "post": {
        "tags": [
          "HateoasGrapes"
        ],
        "summary": "Create a new grape",
        "requestBody": {
          "description": "grape",
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/Grape"
              }
            },
            "text/json": {
              "schema": {
                "$ref": "#/components/schemas/Grape"
              }
            },
            "application/*+json": {
              "schema": {
                "$ref": "#/components/schemas/Grape"
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "Grape is created"
          },
          "500": {
            "description": "Internal Server Error"
          }
        }
      },
      "get": {
        "tags": [
          "HateoasGrapes"
        ],
        "summary": "Get all the grapes",
        "responses": {
          "200": {
            "description": "Returns a list of grapes",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/GrapeIEnumerableHateoasModel"
                }
              }
            }
          },
          "500": {
            "description": "Internal Server Error"
          }
        }
      }
    },
    "/api/v1/hateoas-grapes/{id}": {
      "delete": {
        "tags": [
          "HateoasGrapes"
        ],
        "summary": "Delete a grape",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "description": "grape id",
            "required": true,
            "schema": {
              "type": "integer",
              "description": "grape id",
              "format": "int32"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Deletion is ok"
          },
          "500": {
            "description": "Internal Server Error"
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
      "Grape": {
        "type": "object",
        "properties": {
          "id": {
            "type": "integer",
            "format": "int32"
          },
          "name": {
            "maxLength": 100,
            "type": "string",
            "nullable": true
          },
          "description": {
            "maxLength": 255,
            "type": "string",
            "nullable": true
          }
        },
        "additionalProperties": false
      },
      "Link": {
        "type": "object",
        "properties": {
          "href": {
            "type": "string",
            "nullable": true
          },
          "rel": {
            "type": "string",
            "nullable": true
          },
          "method": {
            "type": "string",
            "nullable": true
          }
        },
        "additionalProperties": false
      },
      "GrapeIEnumerableHateoasModel": {
        "type": "object",
        "properties": {
          "data": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Grape"
            },
            "nullable": true
          },
          "links": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Link"
            },
            "nullable": true
          }
        },
        "additionalProperties": false
      }
    }
  },
  "externalDocs": {
    "description": "Open API Specification (OAS)",
    "url": "http://spec.openapis.org/oas/v3.0.3"
  }
}
```

<br/>

### References:

HTTP/1.1 Semantic: https://httpwg.org/specs/rfc7231.html

JSON viewer: http://jsonviewer.stack.hu/

OpenAPI Specification V3.0.3: http://spec.openapis.org/oas/v3.0.3

