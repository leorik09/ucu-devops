ARG python=python:3.10-slim

FROM ${python} AS build
RUN python3 -m venv /venv
ENV PATH=/venv/bin:$PATH
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

FROM ${python}
RUN groupadd -r flaskuser && \
    useradd --no-log-init -r -g flaskuser flaskuser

COPY --from=build /venv /venv
COPY . .
ENV PATH=/venv/bin:$PATH

USER flaskuser:flaskuser
EXPOSE 8000

CMD ["python", "main.py"]
