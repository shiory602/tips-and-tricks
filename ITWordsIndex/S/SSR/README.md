# SSR
Server-side Rendering
A method of generating and rendering HTML on the server side.

## Rendering process flow
HTTP request is sent from browser to server. 2.
The server retrieves values from the database. 3.
3. server executes JS and converts to HTML file using components, template engine, etc. 4.
4. return to the browser as HTML

In Angular and React, the browser contains a mechanism for constructing the HTML that was previously running on the server side.

## Advantages of Server Side Rendering
- Search engine crawlers directly analyze fully rendered pages, which is good for SEO.
- Because the HTML is generated on the server side, page display (first load) is faster.

## Disadvantages
- Increases the burden on the server side.
- A server capable of running Node.js is required.

[Summary of the differences, mechanisms, and characteristics of SPA, SSR, and Jamstack](https://mintaku-blog.net/spa-ssr/)