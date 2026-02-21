# Lab 3 - Web Technologies
API: RandomDuck (random-d.uk) using POSTMAN and HTTPie.

## Contents

- `RandomDuck.postman_environment.json` — environment variables
- `Happy Path.postman_collection.json` — successful requests
- `Errores intencionales.postman_collection.json` — intentional errors (404, 400, 401, 403)
- `solicitud real.postman_collection.json` — real use case request
- `httpie-commands.md` — equivalent HTTPie commands
- `API_ONBOARDING_REPORT.md` — documentation and response evidence

## Chosen API

RandomDuck is a free, public REST API with no authentication required.
It returns random duck photos and GIFs, and includes a special
`/http/:code` endpoint that returns a duck representing each HTTP
status code.
