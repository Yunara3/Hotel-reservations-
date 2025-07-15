# Hotel-reservations-
Python

import datetime
from datetime import datetime

class HotelReservationSystem:
    def __init__(self):
        self.room_types = [
            "Single room",
            "Double room",
            "Triple room",
            "Quad",
            "Queen room",
            "King room",
        ]
        self.room_prices = {
            "Single room": 300,
            "Double room": 500,
            "Triple room": 700,
            "Quad": 800,
            "Queen room": 1200,
            "King room": 1500,
        }
        self.reservations = []

    def show_room_menu(self):
        print("Available Room Types:")
        for idx, room in enumerate(self.room_types, 1):
            print(f"{idx}. {room} - PHP {self.room_prices[room]} per night")

    def calculate_nights(self, check_in, check_out):
        try:
            in_date = datetime.strptime(check_in, "%Y-%m-%d")
            out_date = datetime.strptime(check_out, "%Y-%m-%d")
            nights = (out_date - in_date).days
            return max(nights, 1)
        except Exception:
            return 1

    def make_reservation(self):
        self.show_room_menu()
        while True:
            try:
                room_choice = int(input("\nSelect room type by number: "))
                if 1 <= room_choice <= len(self.room_types):
                    selected_room_type = self.room_types[room_choice - 1]
                    selected_price = self.room_prices[selected_room_type]
                    break
                else:
                    print(f"Please enter a number between 1 and {len(self.room_types)}.")
            except ValueError:
                print("Invalid input. Please enter a valid number.")

        guest_name = input("Enter guest name: ")
        check_in = input("Enter check-in date (YYYY-MM-DD): ")
        check_out = input("Enter check-out date (YYYY-MM-DD): ")
        nights = self.calculate_nights(check_in, check_out)
        total_cost = selected_price * nights

        reservation_details = {
            "guest_name": guest_name,
            "room_type": selected_room_type,
            "check_in": check_in,
            "check_out": check_out,
            "price_per_night": selected_price,
            "nights": nights,
            "total_cost": total_cost,
            "status": "Confirmed",
        }
        self.reservations.append(reservation_details)
        self.confirm_reservation(reservation_details)

    def confirm_reservation(self, reservation_details):
        print("\nReservation confirmed:")
        print(f"Guest Name: {reservation_details['guest_name']}")
        print(f"Room Type: {reservation_details['room_type']}")
        print(f"Check-in: {reservation_details['check_in']}")
        print(f"Check-out: {reservation_details['check_out']}")
        print(f"Price per Night: PHP {reservation_details['price_per_night']}")
        print(f"Nights: {reservation_details['nights']}")
        print(f"Total Cost: PHP {reservation_details['total_cost']}")
        print(f"Status: {reservation_details['status']}")

    def view_reservations(self):
        if not self.reservations:
            print("No reservations found.")
        else:
            for idx, reservation in enumerate(self.reservations, 1):
                print(f"\nReservation {idx}:")
                print(f"Guest Name: {reservation['guest_name']}")
                print(f"Room Type: {reservation['room_type']}")
                print(f"Check-in: {reservation['check_in']}")
                print(f"Check-out: {reservation['check_out']}")
                print(f"Price per Night: PHP {reservation['price_per_night']}")
                print(f"Nights: {reservation['nights']}")
                print(f"Total Cost: PHP {reservation['total_cost']}")
                print(f"Status: {reservation['status']}")

def main():
    hotel = HotelReservationSystem()
    while True:
        print("\nHotel Reservation System")
        print("1. Make a Reservation")
        print("2. View Reservations")
        print("3. Exit")
        choice = input("Enter your choice: ")
        if choice == "1":
            hotel.make_reservation()
        elif choice == "2":
            hotel.view_reservations()
        elif choice == "3":
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()

