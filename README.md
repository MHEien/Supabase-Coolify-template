# Supabase x Coolify
Get Supabase at https://supabase.com/
Get Coolify at https://coolify.io/


## Deployment Steps

To deploy Supabase on Coolify, follow these steps:

1. **Clone the repo**
   - The content of the files are mostly the same as the original supabase files, except for a few changes to fit Coolify.
    ```bash
    git clone https://github.com/MHEien/Supabase-Coolify-template.git
    ```
2. **Create a New Project in Coolify**
    - Choose installation by Docker-compose.
    - Copy & Paste the contents of `docker-compose.yml` from this repo into Coolify and save. **DO NOT DEPLOY YET!**
3. ***Move the volumes folder to the location of the docker-compose***
    ```bash
    cd path/to/supabase/docker
    cp -r ./volumes /data/coolify/services/<PROJECTID>/
    ```

4. **In Coolify**
    - Enter developer mode in Environment variables and paste your `.env`.
    - In Storage, verify that the contents of the `./volumes` matches the content from this repo. Copy & Paste where missing.
    - **Coolify does not mark directories by default, you must override this by checking the "Is Directory option".**
    - **The directories are listed below.**
    - **It seems that some times, even when the content in storage is populated, it fails to load. So I recommend clicking save on each one before deploying to verify they save.**

5. **Configure Logs Explorer**
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
