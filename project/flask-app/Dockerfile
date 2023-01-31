FROM python:2.7 as builder

# install node.js and npm
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash - \
 && apt-get install -y nodejs
#creating a working directory
WORKDIR /app
#copy package.json and package-lock.json
COPY package*.json ./
#install dependencies
RUN npm install
COPY . .
RUN npm run build

#multi-stage
FROM python:2.7.18-slim-stretch
COPY --from=builder ./app .
RUN pip install -r requirements.txt
ENTRYPOINT [ "python2", "app.py"]


