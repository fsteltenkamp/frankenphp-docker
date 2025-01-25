# Frankenphp Docker
This Repository contains Dockerfiles for Images using Frankenphp including some addons i needed for personal projects.  
Feel free to use them, dont expect regular Updates though, as i only update them when i need to.  
If you need something updated, feel free to open pull requests.
## Additional Software
I Added the following Software to all images:
- Git
- Zip / Unzip
- Composer
- Nodejs

## Extra Images (tags)
The following tags provide different additional addons and software.
- `<version>-mssql`: 
    - MsSQL Driver
- `<version>-mssql-mysqli`:
    - MsSQL Driver and myqsli instead of pdo_mysql
- `<version>-mysqli`:
    - Mysqli Driver instead of the default pdo_mysql