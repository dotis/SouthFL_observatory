### Notes on use of Copernicus Data Space API 
(scihub has been deprecated)

py code from Deepseek:

import requests

# OAuth2 Token Endpoint
auth_url = "https://identity.dataspace.copernicus.eu/auth/realms/CDSE/protocol/openid-connect/token"

# Your credentials (replace with your Client ID & Secret)
client_id = "your-client-id"
client_secret = "your-client-secret"

# Request token
response = requests.post(
    auth_url,
    data={
        "grant_type": "client_credentials",
        "client_id": client_id,
        "client_secret": client_secret,
    },
    headers={"Content-Type": "application/x-www-form-urlencoded"},
)

access_token = response.json()["access_token"]
print("Access Token:", access_token)





