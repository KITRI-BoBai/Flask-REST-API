## REST-API
> Flask 기반 사용자에게 REST API 제공 예제 😉

### Prerequisite
```sh
$ pip install flask
$ pip install flask-restx
```

### Run API Server
```sh
$ python server.py
```

### Code Description
```py
import csv
from flask import Flask, request
from flask_restx import Api, Resource

# Flask 객체에 API 객체 등록
app = Flask(__name__)
api = Api(app)

# CSV 파일을 Dictionary로 변경
mydict = {}
with open('./bluehouse/TF_submission_2021-09-13 13_40_59.csv', 'r', encoding='utf-8') as input:
    reader = csv.reader(input)
    mydict = {rows[0]:rows[1] for rows in reader}

# '/api/{index}' API 가져오기
@api.route('/api/<string:index>')
class API(Resource):
    def get(self, index):
        return {
            "index": "%s" % index,
            "category": "%s" % mydict[index]
        }

# localhost 80 port에서 서버 구동
if __name__ == "__main__":
    app.run(debug=True, host='0.0.0.0', port=80)
```

### Result
> ![결과](https://user-images.githubusercontent.com/20378368/133106473-77f6aca8-d7aa-40f7-b988-597d8f20e440.png)