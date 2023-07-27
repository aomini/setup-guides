# Development Setup

The project uses SSO which shares domain cookie between each requests. Since, we are on a different domain we need to proxy requests to the `.agora.io` domain or run the dev server on same domain.

## Initial Setup

This step is required which is to create `.env` file for the project. There's a `.env.example` file, copy the content of that file and create a new file `.env` then paste the contents inside of it.
You can also copy this into `.env` if you don't see `.env.example`.

```
NEXT_PUBLIC_API_BASE_URL=http://console-dev.agora.io/console/api/v2
NEXT_PUBLIC_API_V0_BASE_URL=http://console-dev.agora.io/api/v0
NEXT_PUBLIC_CHAT_URL=http://console-micr-sdb.easemob.com:8001/im-console/app-overseas/im-service-en
NEXT_PUBLIC_STRIPE_KEY=pk_test_ZCBKz3J8FUu0hKkA4QryvUn2
NEXT_PUBLIC_STRIPE_SG=pk_test_51JNF2LJn7UkiUReEIc7wQwGmDJsuePMTI6EyJDNNhwU2fRptL0kNjf7zE0yvlj3J3GcbvNltQW1YC8ZKwSAxz0CV00LcbQXbW9
```

**Remember:** the `.env` should be created in the root directory, in the same folder structure level as `.env.example`.

> There are two ways to make the project running. The second step is easier but requires a manual work where as step 1 works flawlessly in linux based systems (ubuntu or macOS).

## 1. Same site local server

In order to keep the site on same domain we need to configure the local domain server. We can do it by editing `/etc/hosts`.
You can use vim or nano editor for editing the file (nano is easier). Remember if you are on mac or linux systems you need to run this command with sudo user.
`sudo vim /etc/hosts` or `vi /etc/hosts` or `sudo nano /etc/hosts`.
Add a line below.

```
127.0.0.1       console-dev.agora.io
```

Now, save and exit. In vim, we can do `esc` then `:wq`.
We now have the same subdomain similar to sso which runs in `.agora.io` domain.
The local server environments should use `console-staging.agora.io`.

### Running the project with same domain

> `yarn dev -p 80`
> In the browser, first go to https://console-staging.agora.io then login.
> Now, in another tab go to http://console-dev.agora.io. Keep in mind it's http.
> We will automatically login in the system.

## 2. Different domain

In case of different domain, we don't have to set anything in the `/etc/hosts`.

### Running the project with different domain

> `yarn dev` should spin up the server in port 3000 generally.
> In the browser, first go to https://console-staging.agora.io then login.
> Open the developers tool and navigate to cookie section.
> Find `agora-dashboard-staging` cookie and copy the value.
> Now, in the browser go to http://localhost:3000 (assuming the project is running in 3000 which is by default)
> Then, open the developers tool and create a cookie with name `agora-dashboard-staging` and paste the value that we copied earlier.
> Refresh the page then it should be working.
