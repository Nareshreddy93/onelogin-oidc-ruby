# OneLogin OpenId Connect Implicit Flow Sample

This sample is default Rails 5 app that makes use of the [openid-connect](https://github.com/nov/openid_connect) gem for managing user authentication.

The sample tries to keep everything as simple as possible so only
implements
* Login - redirecting users to OneLogin for authentication
* Logout - destroying the local session and revoking the token at OneLogin
* User Info - fetching profile information from OneLogin

The majority of the logic is found in the `sessions_controller.rb` and `sessions_helper.rb`.

The `dashboard#index` is a protected page to prove the authentication works and creates a session. You will need to be authenticated to view it.

## Setup
In order to run this sample you need to setup an OpenId Connect
app in your OneLogin Admin portal.

If you don't have a OneLogin developer account [you can sign up here](https://www.onelogin.com/developer-signup).

1. Clone this repo
2. Update `app/helpers/sessions_helper.rb` with the **client_id** and
**client_secret** you obtained from OneLogin as well as the **subdomain**
of your OneLogin account and the Redirect Uri of your local site.

You need to make sure that this matches what you specified as the
Redirect Uri when you setup your OIDC app connector in the OneLogin portal.

## Run
From the command line run
```
> bundle install
> rails s
```

### Local testing
By default these samples will run on `http://localhost:3000` but since localhost
is not supported by the OIDC spec you will need to use a tool like [Ngrok](https://ngrok.com/)
for local testing.

Install ngrok using `npm install -g ngrok` then run `ngrok http 3000` and Ngrok will
give you a public HTTPS url that you can browse to and see your local app.

You will need to set this Ngrok url as the **redirect_uri** in your OneLogin OIDC app
via the Admin portal and also in your `.env` file.