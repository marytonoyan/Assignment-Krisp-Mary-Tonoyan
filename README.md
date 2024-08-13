
# Recommendation Service

## Overview

This service provides recommendations based on the `model_name` and `viewer_id` parameters. It is implemented using Flask and Flask-RESTful.

## Code

Here is the implementation of the recommendation service:

```python
from flask import Flask, jsonify, request
from flask_restful import Api, Resource
import random

app = Flask(__name__)
api = Api(app)

def generate_rec(model_name, viewer_id):
    if not model_name or not viewer_id:
        return {"error": "Model name and viewer ID are required"}, 400

    random_number = random.randint(1, 100)
    result = {
        "reason": model_name,
        "result": random_number
    }
    return result

class RecommendationResource(Resource):
    def get(self):
        data = request.args
        model_name = data.get("model_name")
        viewer_id = data.get("viewer_id")
        result = generate_rec(model_name, viewer_id)
        return jsonify(result)

api.add_resource(RecommendationResource, '/recommendation')

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)

