# Recursive/Flatten JSONs REST service
Mule4 example app. Able to convert recursive to flatten JSON structure and vice versa.

Service is able to:
- receives a recursive JSON structure and returns the flattened version;
- receives a flatten JSON structure and returns the recursive version.

# Technology
- RAML 1.0
- Mule 4.4.0EE

# To run application: 
Checkout from this repository and import into Anypoint Studio 7.X.X.

# Exposed endpoints:
By default, service will run on **http://localhost:8081** </br>
Following endpoints will be exposed:
| Methods | Urls            | Action                                                             |
|---------|-----------------|--------------------------------------------------------------------|
| GET     | /console        | Gives access to the generated documentation for the API            |
| POST    | /api/recursive  | Receives a recursive data structure and returns the flattened one  |
| POST    | /api/flatten    | Receives a flattened data structure and returnes the recursive one |

# Examples
**Example 1:** GET http://localhost:8081/console/ </br>
Run in browser or REST client tool (e.g. Insomnia, Postman...) to open generated documentation for the API. </br>
![Screenshot 2023-03-15 at 10 17 20](https://user-images.githubusercontent.com/82412662/225263273-9af387fb-d83f-4f47-83f3-fbd19564520b.png)

To be able to create a flat or recursive structure, our data must have pre-defined attributes that allow us to determine the location of a specific object.
These attributes are defined as 'parentLevelId' and 'childLevelId' in our case. </br>

**Example 2:** POST http://localhost:8081/api/recursive </br>
Request body:
```
[
  {
    "id": "T01",
    "name": "Truck",
    "childLevelId": 1000,
    "unit": [
      {
        "id": "PL01",
        "name": "Palette",
        "parentLevelId": 1000,
        "childLevelId": 1001,
        "unit": [
          {
            "id": "BO01",
            "name": "Box",
            "parentLevelId": 1001,
            "childLevelId": 1002,
            "unit": [
              {
                "id": "BA01",
                "name": "Bag",
                "parentLevelId": 1002,
                "childLevelId": 1003,
                "unit": [
                  {
                    "id": "TS01",
                    "name": "T-shirt",
                    "parentLevelId": 1003,
                    "childLevelId": 1004
                  }
                ]
              }
            ]
          }
        ]
      }
    ]
  },
  {
    "id": "T02",
    "name": "Truck",
    "childLevelId": 2000,
    "unit": [
      {
        "id": "PL02",
        "name": "Palette",
        "parentLevelId": 2000,
        "childLevelId": 2001,
        "unit": [
          {
            "id": "BO02",
            "name": "Box",
            "parentLevelId": 2001,
            "childLevelId": 2002,
            "unit": [
              {
                "id": "BA02",
                "name": "Bag",
                "parentLevelId": 2002,
                "childLevelId": 2003,
                "unit": [
                  {
                    "id": "TS02",
                    "name": "T-shirt",
                    "parentLevelId": 2003,
                    "childLevelId": 2004
                  }
                ]
              }
            ]
          }
        ]
      }
    ]
  }
]
```
Response: 200 OK. <br/>
Response body:
```
[
  {
    "id": "T01",
    "name": "Truck",
    "childLevelId": 1000
  },
  {
    "id": "PL01",
    "name": "Palette",
    "parentLevelId": 1000,
    "childLevelId": 1001
  },
  {
    "id": "BO01",
    "name": "Box",
    "parentLevelId": 1001,
    "childLevelId": 1002
  },
  {
    "id": "BA01",
    "name": "Bag",
    "parentLevelId": 1002,
    "childLevelId": 1003
  },
  {
    "id": "TS01",
    "name": "T-shirt",
    "parentLevelId": 1003,
    "childLevelId": 1004
  },
  {
    "id": "T02",
    "name": "Truck",
    "childLevelId": 2000
  },
  {
    "id": "PL02",
    "name": "Palette",
    "parentLevelId": 2000,
    "childLevelId": 2001
  },
  {
    "id": "BO02",
    "name": "Box",
    "parentLevelId": 2001,
    "childLevelId": 2002
  },
  {
    "id": "BA02",
    "name": "Bag",
    "parentLevelId": 2002,
    "childLevelId": 2003
  },
  {
    "id": "TS02",
    "name": "T-shirt",
    "parentLevelId": 2003,
    "childLevelId": 2004
  }
]
```
**Example 3:** POST http://localhost:8081/api/flatten </br>
Request body:
```
[
  {
    "id": "T01",
    "name": "Truck",
    "childLevelId": 1000
  },
  {
    "id": "PL01",
    "name": "Palette",
    "parentLevelId": 1000,
    "childLevelId": 1001
  },
  {
    "id": "BO01",
    "name": "Box",
    "parentLevelId": 1001,
    "childLevelId": 1002
  },
  {
    "id": "BA01",
    "name": "Bag",
    "parentLevelId": 1002,
    "childLevelId": 1003
  },
  {
    "id": "TS01",
    "name": "T-shirt",
    "parentLevelId": 1003,
    "childLevelId": 1004
  },
  {
    "id": "T02",
    "name": "Truck",
    "childLevelId": 2000
  },
  {
    "id": "PL02",
    "name": "Palette",
    "parentLevelId": 2000,
    "childLevelId": 2001
  },
  {
    "id": "BO02",
    "name": "Box",
    "parentLevelId": 2001,
    "childLevelId": 2002
  },
  {
    "id": "BA02",
    "name": "Bag",
    "parentLevelId": 2002,
    "childLevelId": 2003
  },
  {
    "id": "TS02",
    "name": "T-shirt",
    "parentLevelId": 2003,
    "childLevelId": 2004
  }
]
```
Response: 200 OK. <br/>
Response body:
```
[
  {
    "id": "T01",
    "name": "Truck",
    "childLevelId": 1000,
    "unit": [
      {
        "id": "PL01",
        "name": "Palette",
        "parentLevelId": 1000,
        "childLevelId": 1001,
        "unit": [
          {
            "id": "BO01",
            "name": "Box",
            "parentLevelId": 1001,
            "childLevelId": 1002,
            "unit": [
              {
                "id": "BA01",
                "name": "Bag",
                "parentLevelId": 1002,
                "childLevelId": 1003,
                "unit": [
                  {
                    "id": "TS01",
                    "name": "T-shirt",
                    "parentLevelId": 1003,
                    "childLevelId": 1004
                  }
                ]
              }
            ]
          }
        ]
      }
    ]
  },
  {
    "id": "T02",
    "name": "Truck",
    "childLevelId": 2000,
    "unit": [
      {
        "id": "PL02",
        "name": "Palette",
        "parentLevelId": 2000,
        "childLevelId": 2001,
        "unit": [
          {
            "id": "BO02",
            "name": "Box",
            "parentLevelId": 2001,
            "childLevelId": 2002,
            "unit": [
              {
                "id": "BA02",
                "name": "Bag",
                "parentLevelId": 2002,
                "childLevelId": 2003,
                "unit": [
                  {
                    "id": "TS02",
                    "name": "T-shirt",
                    "parentLevelId": 2003,
                    "childLevelId": 2004
                  }
                ]
              }
            ]
          }
        ]
      }
    ]
  }
]
```

# Licence
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
