FROM python:3.12-slim-bookworm
WORKDIR /usr/src/AMWinterhalter
# set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# install system dependencies
RUN apt-get update && apt-get install -y netcat-openbsd

COPY ../requirements.txt .
# install python dependencies
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

# copy project
COPY .. .
RUN sed -i 's/\r$//g' /usr/src/AMWinterhalter/docker/entrypoint.sh
RUN chmod +x /usr/src/AMWinterhalter/docker/entrypoint.sh


EXPOSE 5085


# run entrypoint.sh
ENTRYPOINT ["/usr/src/AMWinterhalter/docker/entrypoint.sh"]
# gunicorn
CMD ["gunicorn", "--config", "gunicorn-cfg.py", "core.wsgi"]
