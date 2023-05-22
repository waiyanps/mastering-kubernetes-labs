FROM python:3.6.3

WORKDIR /app

ENV BIND_PORT 5001
ENV REDIS_HOST localhost
ENV REDIS_PORT 6379

COPY ./requirements.txt /app/requirements.txt
RUN pip install --no-cache-dir --upgrade pip && pip install -r /app/requirements.txt

COPY ./app.py /app/app.py
EXPOSE ${BIND_PORT}

CMD [ "python", "/app/app.py" ]