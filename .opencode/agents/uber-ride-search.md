---
description: Search for an uber ride
model: xai/grok-4.3
mode: subagent
---

## Search for a Ride

Use the following method to create a URL to navigate to when searching for a ride:

```
def create_uber_drop_url(pickup: dict, dropoff: dict) -> str:
    """
    Creates a Uber mobile deep link URL for a trip with given pickup and dropoff locations.
    
    Args:
        pickup (dict): Dictionary containing pickup location details
        dropoff (dict): Dictionary containing dropoff location details
    
    Returns:
        str: The complete Uber deep link URL
    """
    base_url = "https://m.uber.com/go/drop"

    # Encode dropoff as drop[0]
    drop_json = json.dumps(dropoff, separators=(',', ':'))
    drop_encoded = urllib.parse.quote(drop_json)

    # Encode pickup
    pickup_json = json.dumps(pickup, separators=(',', ':'))
    pickup_encoded = urllib.parse.quote(pickup_json)

    # Build the full URL
    url = f"{base_url}?drop%5B0%5D={drop_encoded}&pickup={pickup_encoded}"
    return url

# Example usage
if __name__ == "__main__":
    pickup_example = {
        "addressLine1": "50 Jones St",
        "addressLine2": "San Francisco, CA",
        "id": "21a269af-c4fc-5505-0e29-7e846426726c",
        "source": "SEARCH",
        "latitude": 37.7816233,
        "longitude": -122.41214,
        "provider": "uber_places"
    }

    dropoff_example = {
        "addressLine1": "333 Bush St",
        "addressLine2": "San Francisco, CA",
        "id": "b9354d21-ab8c-cc67-f1db-92f770e0d0a1",
        "source": "SEARCH",
        "latitude": 37.7908631,
        "longitude": -122.4032156,
        "provider": "uber_places"
    }

    url = create_uber_drop_url(pickup_example, dropoff_example)
    print(url)
```

Only print the URL for other agents to reference.
