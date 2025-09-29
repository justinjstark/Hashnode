---
title: "JotForm API and Workspaces"
datePublished: Mon Sep 29 2025 19:57:42 GMT+0000 (Coordinated Universal Time)
cuid: cmg5jvyg4000302i6e48nes1c
slug: jotform-api-and-workspaces
tags: software-engineering

---

If you are using JotForm Enterprise with Workspaces and you want to query forms for a workspace, you have to use the header `jf-team-id`.

## Getting the Team ID

If you aren’t sure of your team ID, you can issue a GET request to:  
  
`https://{{your-subdomain}}.jotform.com/API/team/user/me?apiKey={{your-api-key}}`

You can alternatively put the API key in the header with key `APIKEY`.

The response you will get looks like this:

```json
{
    "responseCode": 200,
    "message": "success",
    "content": [
        {
            "id": "123456789",
            "name": "Team 1",
            "teamspace_id": "1212121212121212",
            "creator": "me",
            "owner": "me",
            "slug": "team1",
            "created_at": "2025-09-29 18:54:56",
            "updated_at": null
        }
    ]
}
```

The `id`, in this case `123456789`, is the ID you will pass in the `jf-team-id` in future requests. You want the `id` and not the `teamspace_id`.

## Making a Request

As an example, to get forms in this workspace, make a GET request to:

`https://{{your-subdomain}}.jotform.com/API/user/forms`

with the headers

```json
APIKEY: {{your-api-key}}
jf-team-id: {{id-from-above}}
```

And you will get back the forms for this workspace.