<p align="center">
  restQL-clojure allows to run <strong>restQL</strong> queries directly in the JVM, making easy to fetch information from multiple services in the most efficient manner
</p>


<p align="center">
  <a href="https://travis-ci.org/B2W-BIT/restQL-clojure" title="restQL on travis-ci">
    <img src="https://travis-ci.org/B2W-BIT/restQL-clojure.svg?branch=master" alt="restQL on travis-ci">
  </a>
</p>

## Getting Started

### Installation

Add restQL dependency to your project

**Lein**

```
[b2wdigital/restql-core "2.4.0"]
```

**NPM**

```shell
npm i @b2wdigital/restql
```

### First query

**Clojure**
```clojure
(require '[restql.core.api.restql :as restql])
(restql/execute-query :mappings { :user "http://your.api.url/users/:name" } :query "from user with name = $name" :params { :name "Duke Nukem" } )
```

**Node**
```js
var restlq = require('@b2wdigital/restql')

// executeQuery(mappings, query, params, options) => <Promise>
restql
  .executeQuery(
    {user: "http://your.api.url/users/:name"},
    "from user with name = $name",
    { name: "Duke Nukem" })
  .then(response => console.log(response))
  .catch(error => console.log(error))
```

In the example above restQL will call user API passing "Duke Nukem" in the name param.

## Our query language
The clause order matters when making restQL queries. The following is a full reference to the query syntax, available clauses and order.

```
[ [ use modifier = value ] ]

METHOD resource-name [as some-alias] [in some-resource]
  [ headers HEADERS ]
  [ timeout INTEGER_VALUE ]
  [ with WITH_CLAUSES ]
  [ [only FILTERS] OR [hidden] ]
  [ [ignore-errors] ]
```
e.g:
```restQL
from search
    with
        role = "hero"

from hero as heroList
    with
        name = search.results.name
```
Learn more about [**restQL** query language](http://docs.restql.b2w.io/#/restql/queryLang)

# Links
* [Docs](http://docs.restql.b2w.io)
* [Code API](https://cljdoc.org/d/b2wdigital/restql-core): [restQL-clojure](https://github.com/B2W-BIT/restQL-clojure) code documentation
* [restQL-clojure](https://github.com/B2W-BIT/restQL-clojure): If you want to embed restQL directly into your Clojure application,
* [restQL-java](https://github.com/B2W-BIT/restQL-java): If you want to embed restQL directly into your Java application,
* [restQL-manager](https://github.com/B2W-BIT/restQL-manager): To manage saved queries and resources endpoints. restQL-manager requires a MongoDB instance.
* [Tackling microservice query complexity](https://medium.com/b2w-engineering/restql-tackling-microservice-query-complexity-27def5d09b40): Project motivation and history

## Reach the community
* [#restql](https://clojurians.slack.com/messages/C8S6EG8BF): [clojurians](https://clojurians.slack.com) restQL Slack channel
* [@restQL](https://t.me/restQL): restQL Telegram Group

## Who's talking about restQL

* [infoQ: restQL, a Microservices Query Language, Released on GitHub](https://www.infoq.com/news/2018/01/restql-released)
* [infoQ: 微服务查询语言restQL已在GitHub上发布](http://www.infoq.com/cn/news/2018/01/restql-released)
* [OSDN Mag: マイクロサービスクエリ言語「restQL 2.3」公開](https://mag.osdn.jp/18/01/12/160000)
* [Build API's w/ GraphQL, RestQL or RESTful?](https://www.youtube.com/watch?v=OeUGswoYrvA)

## License

Copyright © 2016-2019 B2W Digital

Distributed under the MIT License.
