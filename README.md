# datastore.py
from google.oauth2 import service_account
from google.cloud import datastore
from datetime import datetime

#Project ID where Datastore is located
PROJECT_ID = "hsc2020-01"

# Credentials file
GOOGLE_APPLICATION_CREDENTIALS_PATH = "C:/Users/Saung IT - 003/Desktop/Latihan_13.json"
# Create credentials object
credentials = service_account.Credentials.from_service_account_file(GOOGLE_APPLICATION_CREDENTIALS_PATH)


def simpan(temp):
    # Create a client to access the datastore
    client = datastore.Client(project=PROJECT_ID, credentials=credentials)

    # Create a new key to store a new entity
    newKey = client.key("Suhu")

    # Create a new entity
    newEntity = datastore.Entity(newKey)
    
    # Fill in its data
    newEntity.update({
        "created": datetime.now(),
        "suhu": temp,
    })

    # Store it
    client.put(newEntity)


simpan(15)
