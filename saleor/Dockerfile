FROM python:3.6-alpine as build-python

WORKDIR /app
ADD requirements.txt /app/
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
RUN apk add --no-cache libffi-dev postgresql-dev python3-dev build-base cairo-dev cairo cairo-tools \
                       # Pillow dependencies
                       jpeg-dev \
                       zlib-dev \
                       freetype-dev \
                       lcms2-dev \
                       openjpeg-dev \
                       tiff-dev \
                       tk-dev \
                       tcl-dev

ENV REFRESHED_AT 2019-3-17
RUN pip install --no-cache-dir -i https://pypi.tuna.tsinghua.edu.cn/simple -r requirements.txt
ADD . /app
ENV PYTHONUNBUFFERED 1
ENV DJANGO_SETTINGS_MODULE saleor.settings
EXPOSE 8000
CMD ["gunicorn", "-b 0.0.0.0:8000", "-w 8" , "saleor.wsgi"]
