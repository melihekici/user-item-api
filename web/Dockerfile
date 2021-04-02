FROM python:3
WORKDIR /usr/src/app
COPY requirements.txt .

RUN pip3 uninstall py_jwt_extended
RUN pip3 uninstall jwt
RUN pip3 install PyJWT==1.7.1

RUN pip3 install --no-cache-dir -r requirements.txt
COPY . .

CMD [ "python3", "app.py"]