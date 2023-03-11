# Week 2 — Distributed Tracing

#### Instrumenting using Honeycomb
login to your honeycomb account [Honeycomb account](https://ui.honeycomb.io/login)
set env variables in the environemnt as the following 

```bash
export HONEYCOMB_API_KEY="<my_api_key>"
export HONEYCOMB_SERVICE_NAME="Cruddur"
```
make those values persistent in gitpod:
```bash
gp env HONEYCOMB_API_KEY="<my_api_key>"
gp env HONEYCOMB_SERVICE_NAME="Cruddur"
```
- Update  `docker-compose.yml` file with the following : 
``` sh
OTEL_SERVICE_NAME: "${HONEYCOMB_SERVICE_NAME}"
OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=${HONEYCOMB_API_KEY}"
```
- add the following file to the requirments file :
```python
pip install -r requirements.txt
```

- I added the following imports to my `app.py` file:

```python
from opentelemetry import trace
from opentelemetry.instrumentation.flask import FlaskInstrumentor
from opentelemetry.instrumentation.requests import RequestsInstrumentor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor

```

- Initialize tracing and an exporter that can send data to Honeycomb by adding those line to the `app.py`file :

```python

provider = TracerProvider()
processor = BatchSpanProcessor(OTLPSpanExporter())
provider.add_span_processor(processor)

```


- Testing this works... within my `frontend-react-js` directory, I did an `npm install` then cd'd one level back and then `docker compose up` to start both the frontend & backend apps.

