# Lord Of The Rings API

## Installation

```shell
pip install rimvydas-zilinskas-lotr-api
```

## Prerequisites

To use this library, you have to obtain an API key from https://the-one-api.dev/

Once registered, store your API key securely

## Usage

To start using our SDK you will need to initialize a new API client with your newly created API token as in the example below:

```python
from lotr_api import API

api = API("generated-api-token")

response = api.get_books()
response.docs

# [
#     {
#         "_id": "5cf5805fb53e011a64671582",
#         "name": "The Fellowship Of The Ring"
#     },
#     {
#         "_id": "5cf58077b53e011a64671583",
#         "name": "The Two Towers"
#     },
#     {
#         "_id": "5cf58080b53e011a64671584",
#         "name": "The Return Of The King"
#     }
# ]
```

### Resources

You can retrieve the following resources using our library:

- Books
  - Chapters
- Movies
  - Quotes
- Characters
  - Quotes
- Quotes
- Chapters

The API class has multiple get methods generated for each resource.

To get a list of resources, follow the following method naming:

```
get_*s(**filters)

e.g.
api.get_movies(academyAwardWins__gt=10)
```

To get resources of type by ID:

```
get_*(identifier, **filters)

e.g.
api.get_movie("5cd95395de30eff6ebccde56")
```

To get a nested resource list:

```
get_{base_resource}_{nested_resource}s(identifier, **filters)

e.g.

api.get_movie_quotes("5cd95395de30eff6ebccde56")
```

## Filtering

You can filter base resources by value using different methods. We utilize the naming 
conventions coming from Python magic methods to convert them into valid URL queries.

To filter using lookups, you need to append the lookup using `__` (two underscores)
after the field name you wish to filter by.

```
neq - not equal, ex. runtimeInMinutes__neq=100
gt - greater than
gte - greater than or equal
lt - less than
lte - less than or equal
```

## Pagination

Pagination is enabled by design and users of the library can check if dataset was fully
retrieved using `.has_next` method of Response object and easily parse the next using `.has_next` method.

Page number will be overriden in retrieving subsequent responses even if the implementer provided a
page filter argument in the original query.

Use `limit` to limit the amount of resources returned in a single request
