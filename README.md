# TryHotel API

Hello everyone! 👋

This is a small API for practicing network operations in your application, providing information about hotels.

## Features

🔹 **List of Hotels**:
[List of Hotels](https://raw.githubusercontent.com/fightersubmarine/TryHotelApi/main/firstData.json)

🔹 **Detailed Hotel Information**:
[Hotel Information](https://raw.githubusercontent.com/fightersubmarine/TryHotelApi/main/X.json)
- Where `X` is the `id` of the hotel from the list

🔹 **Hotel Image**:
[Hotel Image](https://raw.githubusercontent.com/fightersubmarine/TryHotelApi/main/image/Y)
- Where `Y` is the name of the image

## How to use

###  Get a list of hotels on ```Swift```
```swift
import Foundation

struct Hotel: Codable {
    let id: Int
    let name: String
    // Add other required fields
}

func fetchHotels(completion: @escaping ([Hotel]?) -> Void) {
    let url = URL(string: "https://raw.githubusercontent.com/fightersubmarine/TryHotelApi/main/firstData.json")!
    let session = URLSession.shared

    let task = session.dataTask(with: url) { data, response, error in
        guard error == nil else {
            print("Error: \(error!)")
            completion(nil)
            return
        }

        guard let data = data else {
            print("No data")
            completion(nil)
            return
        }

        do {
            let hotels = try JSONDecoder().decode([Hotel].self, from: data)
            completion(hotels)
        } catch {
            print("Error decoding data: \(error)")
            completion(nil)
        }
    }

    task.resume()
}

// Example of a function call
fetchHotels { hotels in
    if let hotels = hotels {
        for hotel in hotels {
            print("Hotel ID: \(hotel.id), Name: \(hotel.name)")
        }
    } else {
        print("Failed to fetch hotels")
    }
}
```
