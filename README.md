
# Serverless Web App for Student Data Management

This is a serverless web application that allows students to log in, submit their data, and view all submitted records. The app uses a fully serverless architecture leveraging AWS services, including **AWS Lambda**, **DynamoDB**, **S3**, and **API Gateway**. The frontend is built with **HTML** and **CSS**, while the backend logic is handled using **Python**.

---

## 🛠️ Technologies Used

- **Frontend:** HTML, CSS
- **Backend:** Python (AWS Lambda)
- **Database:** AWS DynamoDB
- **Cloud Services:**
  - AWS Lambda
  - AWS API Gateway
  - AWS DynamoDB
  - AWS S3

---

## 🚀 Features

- ✅ Student Login
- ✅ Submit student data (name, email, etc.)
- ✅ View all student records
- ✅ Serverless backend using AWS Lambda
- ✅ REST API via AWS API Gateway
- ✅ No server to manage

---

## 🧱 Architecture

```mermaid
graph TD;
  A[Student Web Browser] --> B[HTML/CSS Frontend (Hosted on S3)];
  B --> C[API Gateway];
  C --> D[AWS Lambda (Python)];
  D --> E[DynamoDB];
  E --> D;
  D --> C;
  C --> B;
````

---

## 📂 Project Structure

```
serverless-web-app/
│
├── frontend/
│   ├── index.html
│   └── styles.css
│
├── lambda/
│   └── handler.py
│
├── api/
│   ├── POST /submit-data
│   └── GET /view-data
│
└── README.md
```

---

## 🧑‍💻 How It Works

### 1. Frontend (HTML/CSS)

* A simple login form allows students to enter their details.
* On form submission, data is sent to AWS API Gateway.

### 2. AWS API Gateway

* Routes incoming HTTP requests to the appropriate AWS Lambda function.

### 3. AWS Lambda (Python)

* Handles form submissions.
* Stores data in DynamoDB or retrieves records.

### 4. DynamoDB

* Serverless NoSQL database for storing student information.

### 5. S3 (Optional)

* Used for hosting the frontend (index.html and styles.css) or storing uploaded files if needed.

---

## 📦 Deployment Instructions

### 1. Upload Frontend to S3

```bash
aws s3 cp frontend/ s3://your-bucket-name/ --recursive
```

### 2. Create DynamoDB Table

* Table name: `Students`
* Primary key: `email` (String)

### 3. Create Lambda Functions

* **submit\_data\_lambda** → Handles POST requests to add data
* **view\_data\_lambda** → Handles GET requests to retrieve all data

Make sure to include the correct IAM permissions:

* `dynamodb:PutItem`
* `dynamodb:Scan`

### 4. Setup API Gateway

* **POST /submit-data** → Linked to `submit_data_lambda`
* **GET /view-data** → Linked to `view_data_lambda`

Enable CORS for both endpoints.

### 5. Connect Frontend to Backend

Update your `index.html` with the correct API Gateway endpoint URLs:

```javascript
fetch("https://your-api-id.execute-api.region.amazonaws.com/submit-data", { ... })
```

---

## 🧪 Sample Lambda Handler (Python)

```python
import json
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Students')

def lambda_handler(event, context):
    data = json.loads(event['body'])
    table.put_item(Item={
        'email': data['email'],
        'name': data['name'],
        'department': data['department']
    })
    return {
        'statusCode': 200,
        'body': json.dumps('Data saved successfully!')
    }
```

---

## 🧾 Sample Output

```json
[
  {
    "email": "john@example.com",
    "name": "John Doe",
    "department": "CSE"
  },
  {
    "email": "jane@example.com",
    "name": "Jane Smith",
    "department": "ECE"
  }
]
```

---

## 📸 Screenshots

### 🖼️ Login Page

![Login Page](https://via.placeholder.com/600x300.png?text=Login+Page)

### 🖼️ Data View Page

![Data View](https://via.placeholder.com/600x300.png?text=Student+Data+Table)

> *Replace the above links with actual screenshots once deployed.*

---

## 📚 Future Improvements

* Add authentication via AWS Cognito
* Enable file uploads (profile images) to S3
* Search and filter functionality in data view
* Input validation and error handling

---

## 📌 Author

**Subhrasis Biswal**
B.Tech CSE Student
[LinkedIn](https://linkedin.com) • [GitHub](https://github.com/Subhrasis-168)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```

---

Let me know if you'd like to:
- Add real screenshot URLs
- Include deployment automation via SAM or CloudFormation
- Modify for AWS Cognito authentication
- Generate PDF version of this README

I can also give you Lambda code templates for submit and view if you want.
```
