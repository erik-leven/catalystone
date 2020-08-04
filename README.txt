Examples:

Non-historic users:
	system config:
		{
		  "_id": "catalystone-users",
		  "type": "system:microservice",
		  "docker": {
		    "environment": {
		      "client_id_user": "",
		      "client_secret_user": "",
		      "get_url": "https://bt.catalystone.com/bouvet/api/v2/export",
		      "grant_type": "client_credentials",
		      "token_url": "https://bt.catalystone.com/bouvet/api/v2/oauth2/token"
		    },
		    "image": "",
		    "port": 5000
		  }
		}
	pipe config:
		{
		  "_id": "catalystone-user-test",
		  "type": "pipe",
		  "source": {
		    "type": "json",
		    "system": "catalystone-users",
		    "url": "user"
		  },
		  "transform": {
		    "type": "dtl",
		    "rules": {
		      "default": [
		        ["add", "_id",
		          ["string", "_S.STANDARD_FIELDS.UNIQUE_IMPORT_ID.value"]]
		      ]
		    }
		  }
		}
Non-historic organizations:
	system config:
		{
		  "_id": "catalystone-org",
		  "type": "system:microservice",
		  "docker": {
		    "environment": {
		      "client_id_org": "",
		      "client_secret_org": "",
		      "get_url": "https://bt.catalystone.com/bouvet/api/v2/export",
		      "grant_type": "client_credentials",
		      "token_url": "https://bt.catalystone.com/bouvet/api/v2/oauth2/token"
		    },
		    "image": "",
		    "port": 5000
		  }
		}
	pipe config:
		{
		  "_id": "catalystone-organization-test",
		  "type": "pipe",
		  "source": {
		    "type": "json",
		    "system": "catalystone-org",
		    "url": "organization"
		  },
		  "transform": {
		    "type": "dtl",
		    "rules": {
		      "default": [
		        ["copy", "*"]
		      ]
		    }
		  }
		}

Historic users:
	system config:
		{
		  "_id": "catalystone-users-historic",
		  "type": "system:microservice",
		  "docker": {
		    "environment": {
		      "api_version": "v3",
		      "client_id_user": "",
		      "client_secret_user": "",
		      "employee_url": "https://bt.catalystone.com/bouvet/api/employees",
		      "grant_type": "client_credentials",
		      "token_url": "https://bt.catalystone.com/bouvet/api/accesstoken"
		    },
		    "image": "",
		    "port": 5000
		  }
		}
	pipe config:
		{
		  "_id": "catalystone-user-historic",
		  "type": "pipe",
		  "source": {
		    "type": "json",
		    "system": "catalystone-users-historic",
		    "url": "user-historic"
		  },
		  "transform": {
		    "type": "dtl",
		    "rules": {
		      "default": [
		        ["add", "_id", "_S.employeeId"],
		        ["copy", "*"]
		      ]
		    }
		  }
		}

