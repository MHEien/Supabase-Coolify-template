# Supabase x Coolify
Get Supabase at https://supabase.com/
Get Coolify at https://coolify.io/


## Deployment Steps

To deploy Supabase on Coolify, follow these steps:

1. **Create a New Project in Coolify**
    - Choose installation by Docker-compose.

2. **Clone this Repository**
    ```bash
    git clone https://github.com/MHEien/Supabase-Coolify-template.git
    ```

3. **Copy and Edit Environment Variables**
    ```bash
    cp ./.env.example .env
    ```

4. **Configure Logs Explorer**
    If you want Logs Explorer to work, navigate to `./volumes/logs/vector.yml` and edit the following section:
    ```yaml
    route:
      kong: '.appname == "kong-y48kg0c"' #Replace "y48kg0c" with your Coolify project ID for all of the routes
      auth: '.appname == "auth-y48kg0c"' 
      rest: '.appname == "rest-y48kg0c"' 
      realtime: '.appname == "realtime-y48kg0c"' 
      storage: '.appname == "storage-y48kg0c"' 
      functions: '.appname == "functions-y48kg0c"' 
      db: '.appname == "db-y48kg0c"'
    ```
    Change the required environment variables.

5. **In Coolify**
    - Copy & Paste the contents of `docker-compose.yml` into Coolify and save. **DO NOT DEPLOY YET!**
    - Enter developer mode in Environment variables and paste your `.env`.
    - In Storage, populate the contents of the `./volumes` from this repo.

6. **Mark as Directory in Storages Section**
    ```
    Storage: /data/coolify/services/y48kg0c/volumes/storage
    Imgproxy: /data/coolify/services/y48kg0c/volumes/storage
    Functions: /data/coolify/services/y48kg0c/volumes/functions
    DB: /data/coolify/services/y48kg0c/volumes/db/data
    ```

7. **Populate Files in Coolify Before Deployment**
    - Files:
        ```
        Kong: /data/coolify/services/y48kg0c/volumes/api/kong.yml
        DB:
        /data/coolify/services/y48kg0c/volumes/db/realtime.sql
        /data/coolify/services/y48kg0c/volumes/db/webhooks.sql
        /data/coolify/services/y48kg0c/volumes/db/roles.sql
        /data/coolify/services/y48kg0c/volumes/db/jwt.sql
        /data/coolify/services/y48kg0c/volumes/db/logs.sql
        /data/coolify/services/y48kg0c/volumes/logs/vector.yml
        ```

8. **Now You Can Deploy!**

## Notes

- Some variables (e.g., Docker socket location, KONG port, and STUDIO port) are hardcoded in `docker-compose.yml` due to not being acquired during build-time.

- FQDN is already set up with KONG in the compose, making all Supabase services accessible through KONG.
