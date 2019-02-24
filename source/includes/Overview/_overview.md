# Overview

## Introduction

The TSheets API (Application Programming Interface) is based on [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) principles. It's very easy to write and test applications. You can use your browser to access URLs, and you can use pretty much any TLS-capable HTTP client in any programming language to interact with the API. The API allows you to query metadata about your account, users, jobcodes, timesheets, GPS points, and custom fields. You can also create timesheets, users, jobcodes, etc.

All access to the API occurs over an TLS-encrypted secure channel, so your API client must support TLS. To ensure data privacy, unencrypted HTTP is not supported.
## Getting Started

The quickest way to get started is to use our [Postman](http://www.getpostman.com/) request collection. The following steps will help you get up and running as quickly as possible. If you prefer, our API can also easily be explored with other tools, like cURL.

### 1) Create an Access Token

 * Login to your TSheets account, or sign up for a free trial
 * Create an API Access token by following the instructions in Obtaining a token
 * Copy the token value for use with the imported collection, below.

### 2) Open the TSheets Postman Collection

<div class="postman-run-button"
data-postman-action="collection/import"
data-postman-var-1="01861e468223de53ba7a"></div>
<script type="text/javascript">
  (function (p,o,s,t,m,a,n) {
    !p[s] && (p[s] = function () { (p[t] || (p[t] = [])).push(arguments); });
    !o.getElementById(s+t) && o.getElementsByTagName("head")[0].appendChild((
      (n = o.createElement("script")),
      (n.id = s+t), (n.async = 1), (n.src = m), n
    ));
  }(window, document, "_pm", "PostmanRunObject", "https://run.pstmn.io/button.js"));
</script>
<style>
  .postman-run-button {
    position: relative;
    left: 30px;
  }
</style>

### 3) Configure the Postman Environment

 * Setup a new environment by clicking the Gear icon at top right
 * Name the new environment _TSheets_ and click _Add_ to create
 * Expand the _GET STARTED_ folder and select the _Environment Setup_ method
 * Select the _Pre-req._ tab and set `tsheets-bearer-token` to the value obtained in step 1 above
 * Click the _Send_ button

### 4) Explore the API

 * Execute any of the requests within the collection
 * Refer to this documentation for the requirements of each method

## Base URL

All URLs referenced in the documentation have the following base:

<code class="standout">https://rest.tsheets.com/api/v1</code>

## Request Throttling

To prevent abuse of the TSheets API, we limit requests to a maximum of 300 calls within any 10 minute time window (subject to change). Rate limiting is primarily considered on a per-connection basis (per access token). If you exceed the current rate limit, you will receive a `429 'Too many requests'` response from our API. You will continue to receive a `429` response until you're out of the current time window. The threshold and time window may adjust dynamically downward if you are found to be abusing the system.

## Helper Libraries

This documentation explains the format for calls to the TSheets API with code snippets in cURL and several other languages. Helper libraries are also available upon request to make it even easier for you to get started with TSheets.

 * [PHP Helper Library](https://github.com/tsheets/api_phplib) (hosted on GitHub)
 * [C#/.NET Helper Library](https://github.com/tsheets/api_dotnet) (hosted on GitHub)
 * [Request a library for your favorite language](mailto:help@tsheets.com?subject=API Helper Library Request)

 While a helper library can make it easier to consume the API, it is certainly not necessary and the API is still very straight-forward to use even without one. Simply use a built-in http class or library for your language of choice.

 * Java, use [URLConnection](http://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) or the [Apache HttpComponents](http://hc.apache.org/)
 * Ruby, use [Net::HTTP](http://www.ruby-doc.org/stdlib-2.1.1/libdoc/net/http/rdoc/Net/HTTP.html)
 * Perl, use [HTTP::Client](http://search.cpan.org/~linc/HTTP-Client-1.51/lib/HTTP/Client.pm)

## Partnership Requests and Information

By default we allow you to connect to 3 additional client accounts (besides your own) via your API application keys. If you are building an integration and are interested in enabling your application for use by any TSheets customer, please fill out the form at the bottom of our [partnerships page](https://www.tsheets.com/partners) and we can help guide you through our simple integration process.

Here are a few of the things we'll be looking for before allowing your application access to our other TSheets customers:

 * Are you obtaining tokens by directing the user through our OAuth flow?
 * Are you storing the API App `client_id` and `client_secret` encrypted?
 * Are you storing OAuth tokens encrypted?
 * Do you have a mechanism in place for refreshing OAuth tokens before they expire - to prevent people from needing to log in again?
 * If you are unable to refresh the token, what is the user experience for logging in and renewing it?
 * What permissions are required for your app to do its work? Are you checking those permissions for the user tied to the OAuth token - and not just assuming you'll have it?
 * When checking for changes to data, are you using the [`last_modified_timestamps`](#last-modified) endpoint?
 * How are changes to data being checked from your app? Polling? Manually? Both? If you're polling, how often?
 * If client doesn't have a TSheets account, are you utilizing the account creation mechanism available via the OAuth flow?
 * On initial sync, are you getting all data? On subsequent syncs, are you utilizing last_modified times to pull data?
 * When editing or creating multiple objects, are you doing so via batch operations (i.e. up to 50 with one request vs. a separate request for each)?

## Getting Help

If you encounter any problems consuming the API or have suggestions please feel free to contact us at [help@tsheets.com](mailto:help@tsheets.com)