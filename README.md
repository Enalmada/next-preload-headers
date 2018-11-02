# next-preload-headers

[![npm version](https://badge.fury.io/js/next-preload-headers.svg)](https://badge.fury.io/js/next-preload-headers)

next-routes helper function copies link preload tags in head of initial response into link header where
proxy will server push them.  This significantly decreases the initial "time to interactive" latency for first time
users.

All routes that are server push enabled must be defined in the next-routes file.

TODO: 
- send/check a cookie with buildId so we know if resources need to be pushed for this build
- figure out how to make this work without next-routes

## Usage
Add it to the express app like this:

```
const nextPreloadHeaders = require('next-preload-headers')
const routes = require("./routes");

const nextPreloadHeadersRouterHandler = routes.getRequestHandler(app, ({req, res, route, query}) => {
        nextPreloadHeaders(app, req, res, route.page, query);
    }
);

const app = express()

app.use(nextPreloadHeadersRouterHandler)
```
