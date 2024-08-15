# MongoDB Atlas User Migration Tool

When migrating to MongoDB Atlas, tools like [Cluster-to-Cluster Sync](https://www.mongodb.com/docs/cluster-to-cluster-sync/current/), [Live Migrate](https://www.mongodb.com/docs/atlas/import/live-import/), and [mongomirror](https://www.mongodb.com/docs/atlas/import/mongomirror/) are invaluable. However, these tools do not cover the migration of user and role data.

This Python script fills that gap by helping you migrate your existing database users and roles to MongoDB Atlas. Please note that it cannot migrate user passwords directly; instead, the script generates random passwords and saves them to a `users.txt` file.

## How It Works

- **Fetch Users and Roles:** The script uses the [Python driver](https://www.mongodb.com/docs/drivers/python-drivers/#python-driver) to retrieve your current users and roles from the source database.
- **Create Users on Atlas:** Since MongoDB Atlas [doesn’t support](https://www.mongodb.com/docs/atlas/unsupported-commands/) the [createUser](https://www.mongodb.com/docs/manual/reference/command/createUser/#dbcmd.createUser) command, the script uses the [Database Users](https://www.mongodb.com/docs/atlas/reference/api-resources-spec/v2/#tag/Database-Users) REST API to create users.

## Usage
1. **Install Dependencies:**

   ```bash
   pip install -r requirements.txt

2. **Configure Parameters:**

   Populate the params.py file with your credentials. You’ll need an [Atlas Organization API Key](https://www.mongodb.com/docs/atlas/configure-api-access/#create-an-api-key-in-an-organization).

```bash
# Source Database
source_conn_string = "<Application connection string>"
source_database = 'admin'

# Atlas REST API Credentials
target_project_id = '<Project ID found under Atlas Project Settings>'
target_api_public_key = '<API Public Key>'
target_api_private_key = '<API Private Key>'

   
