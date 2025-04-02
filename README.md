# horse-breed-registry
import json

class HorseBreedRegistry:
    def __init__(self, file_name="horse_breeds.json"):
        self.file_name = file_name
        self.load_data()

    def load_data(self):
        """Load horse breed data from a file or create a new one."""
        try:
            with open(self.file_name, "r", encoding="utf-8") as file:
                self.breeds = json.load(file)
        except (FileNotFoundError, json.JSONDecodeError):
            self.breeds = {}

    def save_data(self):
        """Save breed data to a file."""
        with open(self.file_name, "w", encoding="utf-8") as file:
            json.dump(self.breeds, file, indent=4, ensure_ascii=False)

    def add_breed(self, name, origin, characteristics):
        """Add a new horse breed to the registry."""
        self.breeds[name] = {
            "origin": origin,
            "characteristics": characteristics
        }
        self.save_data()
        print(f"Added horse breed: {name}")

    def get_breed(self, name):
        """Retrieve breed information by name."""
        return self.breeds.get(name, "Breed not found.")

    def list_breeds(self):
        """List all stored horse breeds."""
        if not self.breeds:
            print("No breeds recorded yet.")
            return
        for name, data in self.breeds.items():
            print(f"{name} - Origin: {data['origin']} - Characteristics: {data['characteristics']}")

# Example usage
def main():
    registry = HorseBreedRegistry()
    while True:
        print("\n🐎 Horse Breed Registry")
        print("1. Add a Breed")
        print("2. Get Breed Info")
        print("3. List All Breeds")
        print("4. Exit")
        choice = input("Select an option: ")
        
        if choice == "1":
            name = input("Enter breed name: ").strip()
            origin = input("Enter breed origin: ").strip()
            characteristics = input("Enter breed characteristics: ").strip()
            registry.add_breed(name, origin, characteristics)
        elif choice == "2":
            name = input("Enter breed name: ").strip()
            print(registry.get_breed(name))
        elif choice == "3":
            registry.list_breeds()
        elif choice == "4":
            break
        else:
            print("Invalid choice. Try again.")

if __name__ == "__main__":
    main()
rare
