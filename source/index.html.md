---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript
  - csharp

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - users
  - stands
  - importantThirdPartyAPIs

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Makai API
---

# Introduction

Welcome to the Makai API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```javascript
```

```csharp
```

> Make sure to replace `{YOUR_API_KEY}` with your API key.

Makai uses API keys to allow access to the API.

Makai expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: {YOUR_API_KEY}`

<aside class="notice">
You must replace <code>{YOUR_API_KEY}</code> with your personal API key.
</aside>

Makai also uses multiple third party APIs that will be needed to make certain API calls.

<aside class="notice">
These third Pary API Keys should be stored as variables for better protection.
</aside>

