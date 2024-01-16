#include <iostream>
#include <vector>
#include <string>

class Car {
public:
    std::string brand;
    std::string model;
    int year;
    bool available;

    Car(const std::string& brand, const std::string& model, int year)
        : brand(brand), model(model), year(year), available(true) {}

    void displayInfo() const {
        std::cout << "Brand: " << brand << "\nModel: " << model << "\nYear: " << year << "\nAvailable: " << (available ? "Yes" : "No") << "\n\n";
    }
};

class CarRentalSystem {
private:
    std::vector<Car> cars;

public:
    void addCar(const Car& car) {
        cars.push_back(car);
    }

    void displayAllCars() const {
        std::cout << "----- All Cars -----\n";
        for (const Car& car : cars) {
            car.displayInfo();
        }
    }

    void rentCar(const std::string& brand, const std::string& model) {
        for (Car& car : cars) {

            if (car.brand == brand && car.model == model && car.available) {
                car.available = false;
                std::cout << "Car rented successfully!\n";
                return;
            }
        }
        std::cout << "Car not found or not available for rent.\n";
    }

    void returnCar(const std::string& brand, const std::string& model) {
        for (Car& car : cars) {
            if (car.brand == brand && car.model == model && !car.available) {
                car.available = true;
                std::cout << "Car returned successfully!\n";
                return;
            }
        }
        std::cout << "Car not found or already returned.\n";
    }
};

int main() {
    CarRentalSystem rentalSystem;

    // Adding sample cars
    rentalSystem.addCar(Car("toyota", "camry", 2022));
    rentalSystem.addCar(Car("honda", "civic", 2021));
    rentalSystem.addCar(Car("ford", "mustang", 2020));

    int choice;
    do {
        std::cout << "----- Car Rental System -----\n";
        std::cout << "1. Display all cars\n";
        std::cout << "2. Rent a car\n";
        std::cout << "3. Return a car\n";
        std::cout << "4. Exit\n";
        std::cout << "Enter your choice: ";
        std::cin >> choice;

        switch (choice) {
        case 1:
            rentalSystem.displayAllCars();
            break;
        case 2: {
            std::string brand, model;
            std::cout << "Enter the brand of the car: ";
            std::cin >> brand;
            std::cout << "Enter the model of the car: ";
            std::cin >> model;
            rentalSystem.rentCar(brand, model);
            break;
        }
        case 3: {
            std::string brand, model;
            std::cout << "Enter the brand of the car: ";
            std::cin >> brand;
            std::cout << "Enter the model of the car: ";
            std::cin >> model;
            rentalSystem.returnCar(brand, model);
            break;
        }
        case 4:
            std::cout << "Exiting the system.\n";
            break;
        default:
            std::cout << "Invalid choice. Please try again.\n";
            break;
        }
    } while (choice != 4);

    return 0;
}

