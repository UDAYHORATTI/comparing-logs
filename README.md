from datetime import datetime

# Sample logs in the format: 'username timestamp'
logs = [
    "user1 2025-01-14 08:45:00",
    "user2 2025-01-14 08:46:00",
    "user1 2025-01-14 09:00:00",
    "user3 2025-01-14 09:15:00",
    "user2 2025-01-14 09:30:00",
]

# Function to identify unique logins
def identify_unique_logins(logs):
    logins = {}
    
    for log in logs:
        username, timestamp = log.split(" ", 1)
        timestamp = datetime.strptime(timestamp, "%Y-%m-%d %H:%M:%S")
        
        if username not in logins:
            logins[username] = timestamp
        else:
            # If the user logged in again after the first login, update the timestamp
            logins[username] = max(logins[username], timestamp)
    
    return logins

# Get unique logins
unique_logins = identify_unique_logins(logs)
print("Unique Logins:")
for user, timestamp in unique_logins.items():
    print(f"User: {user}, Last Login: {timestamp}")

