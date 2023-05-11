# Lab 4: Fuzzing VAmPI with Mayhem for API (mapi)

In this lab, we will fuzz a vulnerable API using mapi. Our target is VAmPI, a vulnerable API that includes several OWASP top 10 vulnerabilities for APIs.

## Step 1: Clone VAmPI from GitHub

Clone the VAmPI repository from GitHub:

```bash
git clone https://github.com/erev0s/VAmPI.git
```

## Step 2: Build a Docker Image

Build a Docker image from the cloned VAmPI repository:

```bash
docker build -t vampi_docker:latest -f VAmPI/Dockerfile VAmPI
```

## Step 3: Start the API

Start the API using Docker Compose:

```bash
docker-compose -f VAmPI/docker-compose.yaml up -d
```

## Step 4: Create a User and Get a Bearer Token

Create a user in the application:

```bash
curl --location --request POST "http://localhost:5002/users/v1/register" \
--header 'Content-Type: application/json' \
--data-raw '{
    "email":"foo@example.com",
    "username": "foo",
    "password": "bar"
}'
```

Then, login to get a bearer token:

```bash
curl --location --request POST "http://localhost:5002/users/v1/login" \
--header 'Content-Type: application/json' \
--data-raw '{
    "username": "foo",
    "password": "bar"
}'
```

You should receive a response that contains your token.

## Step 5: Export the Token

Export the token to a variable to facilitate the next calls:

```bash
export VAMPI_TOKEN="<your_token>"
```

## Step 6: Scan with Mayhem for API

Use the mapi CLI to start scanning the API:

```bash
mapi run vampi auto ./VAmPI/openapi_specs/openapi3.yml \
  --ignore-endpoint "^GET /createdb$" \
  --header-auth "Authorization: token ${VAMPI_TOKEN}" \
  --url "http://localhost:5002" \
  --html mapi-report.html
```

Some of the options used:

- `--header-auth "Authorization: token ${VAMPI_TOKEN}"`: This uses the API token from the login to authenticate with the API.
- `--ignore-endpoint "^GET /createdb$"`: This prevents the scanner from calling the `/createdb` endpoint, which recreates the database on every call.
- `--html mapi-report.html`: This generates an HTML report with the results of the run.

## Step 7: Review the Results

At the end of the scan, you should see a list of issues. Each issue includes a rule ID, a summary, the HTTP method, and the API endpoint. Review these issues to understand the vulnerabilities in the API.
