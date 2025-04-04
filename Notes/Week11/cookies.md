# Cookie


>[!note]
> All the notes in this section have been taken from the [Wikipedia page about cookies](https://en.wikipedia.org/wiki/HTTP_cookie). If you want an in-depth understand of cookies, then please go ahead and read the page itself. Otherwise, I have picked out the main points from the page that you should understand.

---

## 🤷‍ What are Cookies?

**Definition:** An HTTP cookie (also called web cookie, Internet cookie, browser cookie, or simply cookie) is a small piece of data stored on the user's computer by the web browser while browsing a website. <br>

**Purpose:** 
-  Cookies were designed to be a reliable mechanism for websites to remember stateful information (such as items added in the shopping cart in an online store) or to record the user's browsing activity (including clicking particular buttons, logging in, or recording which pages were visited in the past). 
-  They can also be used to remember pieces of information that the user previously entered into form fields, such as names, addresses, passwords, and payment card numbers.

**Structure**: 
-  _name_ and _value_
-  cookies can also have one or more _attributes_. 

Browsers do not include cookie attributes in requests to the server; they only send the cookie's name and value. Cookie attributes are used by browsers to determine when to delete a cookie, block a cookie or whether to send a cookie to the server.

### 🌐 Domain and Path

The _Domain_ and _Path_ attributes define the scope of the cookie. They tell the browser what website the cookie belongs to.

**Rules**: For security reasons, cookies can only be set on the current resource's top domain and its sub domains, and not for another domain and its sub domains. 

**Example** : The website `digimon.com` cannot set a cookie that has a domain of `pokemon.com` because this would allow the `digimon.com` website to control the cookies of `pokemon.com`.

**Host-only vs. Domain-wide cookies**

If a cookie's _Domain_ and _Path_ attributes are not specified by the server, they default to the domain and path of the resource that was requested.ie If no domain is specified, the cookie is only available for the specific host.

However, in most browsers there is a difference between a cookie set from `pokemon.com` without a domain, and a cookie set with the `pokemon.com` domain. In the former case, the cookie will only be sent for requests to `pokemon.com`, also known as a host-only cookie. In the latter case, all sub domains are also included (for example, `game.pokemon.com` and `tv.pokemon.com`).

**Example**<br>
Below is an example of some `Set-Cookie` HTTP response headers that are sent from a website after a user logged in. The HTTP request was sent to a webpage within the `game.pokemon.com` subdomain:

```http
HTTP/1.0 200 OK
Set-Cookie: pokedexId=123; Path=/pokedex; Expires=Wed, 13 Jan 2023 22:23:01 GMT; Secure; HttpOnly
Set-Cookie: trainerId=456; Domain=.pokemon.com; Path=/; Expires=Wed, 13 Jan 2021 22:23:01 GMT; HttpOnly
Set-Cookie: pokemonId=789; Domain=pokemon.com; Path=/; Expires=Wed, 13 Jan 2021 22:23:01 GMT; Secure; HttpOnly
…
```

-   The first cookie, `pokedexId`, has no _Domain_ attribute, and has a _Path_ attribute set to `/pokedex`. This tells the browser to use the cookie only when requesting pages contained in `game.pokemon.com/pokedex`.
-   The other two cookies, `trainerId` and `pokemonId`, would be used when the browser requests any subdomain in `.pokemon.com` on any path (for example `www.pokemon.com/pokedex`).

### ⏳ Expires and Max-Age

**Expires**  attribute** defines a specific date and time for when the browser should delete the cookie. The date and time are specified in the form `Wdy, DD Mon YYYY HH:MM:SS GMT`.

**Max-Age** attribute can be used to set the cookie's expiration as an interval of seconds in the future, relative to the time the browser received the cookie. Below is an example of three `Set-Cookie` headers that were received from a website after a user logged in:

```http
HTTP/1.0 200 OK
Set-Cookie: pokedexId=123; Expires=Tue, 15 Jan 2023 21:47:38 GMT; Path=/; Domain=.pokemon.com; HttpOnly
Set-Cookie: trainerId=456; Path=/; Domain=.pokemon.com
Set-Cookie: pokemonId=789; Expires=Thu, 01 Jan 1970 00:00:01 GMT; Path=/; Domain=.pokemon.com; HttpOnly
```

-   The first cookie, `pokedexId`, is set to expire sometime on 15 January 2023. It will be used by the client browser until that time.
-   The second cookie, `trainerId`, does not have an expiration date, making it a session cookie. It will be deleted after the user closes their browser.
-   The third cookie, `pokemonId`, has an expiration time in the past. The browser will delete this cookie right away because its expiration time is in the past.
    -   Note that cookie will only be deleted if the domain and path attributes in the `Set-Cookie` field match the values used when the cookie was created.

### 🔒 Secure and HttpOnly

The **Secure** and **HttpOnly** attributes do not have associated values. Rather, the presence of just their attribute names indicates that their behaviors should be enabled.

**Secure** attribute

- Ensures cookies are only sent over HTTPS.
- Prevents transmission over unsecured connections.

It is meant to keep cookie communication limited to encrypted transmission, directing browsers to use cookies only via secure/encrypted connections. However, if a web server sets a cookie with a secure attribute from a non-secure connection, the cookie can still be intercepted when it is sent to the user by man-in-the-middle attacks. Therefore, for maximum security, cookies with the Secure attribute should only be set over a secure connection.

**HttpOnly** attribute

- Prevents access to cookies via JavaScript (reduces XSS attacks).

This attribute directs browsers not to expose cookies through channels other than HTTP (and HTTPS) requests. This means that the cookie cannot be accessed via client-side JavaScript, and therefore cannot be stolen easily via cross-site scripting (a pervasive attack technique).

## 🤔 Why use Cookies?

### 👥 Session Management

One popular use of cookies is for logging into websites. When the user visits a website's login page, the web server typically sends the client a cookie containing a unique session identifier (typically, a long string of random letters and numbers). When the user successfully logs in, the server remembers that that particular session identifier has been authenticated. Because cookies are sent to the server with every request the client makes, that session identifier will be sent back to the server every time the user visits a new page on the website, and the server will grant the user access to its services.

### 💅 Personalization

Cookies can be used to remember information about the user in order to show relevant content to that user over time. For example, a web server might send a cookie containing the username that was last used to log into a website, so that it may be filled in automatically the next time the user logs in.

Many websites use cookies for personalization based on the user's preferences. Users select their preferences by entering them in a web form and submitting the form to the server. The server encodes the preferences in a cookie and sends the cookie back to the browser. This way, every time the user accesses a page on the website, the server can personalize the page according to the user's preferences. 

For example, [DuckDuckGo](https://duckduckgo.com/) (the search engine you ought to be using if you care about your privacy) uses cookies to allow users to set the viewing preferences like the colors of the page.

### 🕵️‍♀️ Tracking

Tracking cookies are used to track users' web browsing habits. This can be demonstrated as follows:

> If the user requests a page of the site, but the request contains no cookie, the server presumes that this is the first page visited by the user. So the server creates a unique identifier (typically a string of random letters and numbers) and sends it as a cookie back to the browser together with the requested page.
>
> From this point on, the cookie will automatically be sent by the browser to the server every time a new page from the site is requested. The server not only sends the page as usual but also stores the URL of the requested page, the date/time of the request, and the cookie in a log file.

By analyzing this log file, it is then possible to find out which pages the user has visited, in what sequence, and for how long.

Corporations exploit users' web habits by tracking cookies to collect information about buying habits. The Wall Street Journal found that America's top fifty websites installed an average of sixty-four pieces of tracking technology onto computers, resulting in a total of 3,180 tracking files. The data can then be collected and sold to bidding corporations.

## ⚙️ How to use Cookies?

### **Server-Side Cookies (Set-Cookie header)**

Cookies are set using the `Set-Cookie` HTTP header, sent in an HTTP response from the web server. This header instructs the web browser to store the cookie and send it back in future requests to the server (the browser will ignore this header if it does not support cookies or has disabled cookies).

As an example, the browser sends its first request for the homepage of the `www.pokemon.com` website:

```http
GET /index.html HTTP/1.1
Host: www.pokemon.com
...
```

The server responds with two `Set-Cookie` headers:

```http
HTTP/1.0 200 OK
Content-type: text/html
Set-Cookie: theme=dark
Set-Cookie: sessionId=abc123; Expires=Wed, 09 Jun 2021 10:18:14 GMT
...
```

The server's HTTP response contains the contents of the website's homepage. But it also instructs the browser to set two cookies:

-   The first, `theme`, is considered to be a session cookie since it does not have an _Expires_ or _Max-Age_ attribute. Session cookies are intended to be deleted by the browser when the browser closes.
-   The second, `sessionId`, is considered to be a persistent cookie since it contains an _Expires_ attribute, which instructs the browser to delete the cookie at a specific date and time.

Next, the browser sends another request to visit the `pokedex.html` page on the website. This request contains a `Cookie` HTTP header, which contains the two cookies that the server instructed the browser to set:

```http
GET /pokedex.html HTTP/1.1
Host: www.pokemon.com
Cookie: theme=dark; sessionId=abc123
…
```

This way, the server knows that this request is related to the previous one. The server would answer by sending the requested page, possibly including more `Set-Cookie` headers in the response in order to add new cookies, modify existing cookies, or delete cookies.

The value of a cookie can be modified by the server by including a `Set-Cookie` header in response to a page request. The browser then replaces the old value with the new value.

### **Client-Side Cookies (JavaScript API)**

Cookies can also be set by client-side JavaScript that runs within the browser. In client-side JavaScript, the object `document.cookie` is used for this purpose. 

**Example:** `document.cookie = 'temperature=20'` creates a cookie of name "temperature" and value "20".

## 🥱 TL;DR

Cookies are arbitrary pieces of data, usually chosen and first sent by the web server, and stored on the client computer by the web browser. The browser then sends them back to the server with every request, introducing states (memory of previous events) into otherwise stateless HTTP transactions. Without cookies, each retrieval of a web page or component of a web page would be an isolated event, largely unrelated to all other page views made by the user on the website. Although cookies are usually set by the web server, they can also be set by the client using a scripting language such as JavaScript (unless the cookie's `HttpOnly` flag is set).