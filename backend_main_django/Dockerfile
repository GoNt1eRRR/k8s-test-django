FROM nginx/unit:1.25.0-python3.9
ENV PYTHONUNBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1

WORKDIR /webapp
COPY requirements.txt /webapp/
RUN apt update && apt install -y python3-pip                                  \
    && pip3 install --no-cache-dir -r requirements.txt                                       \
    && apt remove -y python3-pip                                              \
    && apt autoremove -y                                              \
    && rm -rf /var/lib/apt/lists/*
COPY unit_config.json /docker-entrypoint.d/
COPY src /webapp/src
WORKDIR /webapp/src
ENV SECRET_KEY=empty
ENV ALLOWED_HOSTS=localhost,127.0.0.1
RUN python manage.py collectstatic --noinput
EXPOSE 80
VOLUME ["/media"]