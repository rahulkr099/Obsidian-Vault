# Dockerfile
```
Purpose: creating dockerfile in YAML

Use a lightweight official Node.js image for production
Set working directory inside the container
Copy only package.json & package-lock.json (for faster caching)
Install only production dependencies (no dev dependencies)
Copy remaining source code inside container
Set environment variable for production mode
Expose the port your application will run on
Command to start the server

```
