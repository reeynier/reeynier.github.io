---
layout: post
title:  "Parking Lot Problem"
categories: [ Object-Oriented Design ]
tags: [ C++, OOD ]
similar: [ OOD ]
featured: false
hidden: false
---

<br />

## Description

Design a parking lot using `object-oriented` principles. We will focus on the following set of requirements while designing the parking lot:
1. The parking lot has multiple levels. Each level has multiple rows of spots.
2. The parking lot can park motorcycles, cars, and buses.
3. The parking lot has motorcycle spots, compact spots, and large spots.
4. A motorcycle can park in any spot.
5. A car can park in either a single compact spot or a single large spot.
5. A bus can park in five large spots that are consecutive and within the same row. It cannot park in small spots.


<br />

## C++ Implementation

In the C++ implementation, we create an abstract class Vehicle, from which Car, Bus, and Motorcycle inherit. To handle the different parking spot sizes, we have just one class ParkingSpot which has a member variable indicating the size.

```c
enum VehicleSize { Motorcycle, Compact, Large };

// Vehicle abstract class
class Vehicle {
    vector<ParkingSpot> parkingSpots;
    string licensePlate;
    int spotsNeeded;
    VehicleSize size;

public:
    int getSpotsNeeded() {
        return spotsNeeded;
    }
    VehicleSize getSize() {
        return size;
    }
    // Park vehicle in the spot
    void parkInSpot(ParkingSpot spot) {
        parkingSpots.push_back(spot);
    }
    // Remove vehicle from spot
    // We let the vehicle to call parkingspot's removeVehicle method
    // We don't clear vehicle's parking spots in parkingspot's removeVehicle function
    // This is because vehicle initiate the leaving spot behavior
    void clearSpots() {
        for (int i = 0; i < parkingSpots.size(); i ++) {
            parkingSpots[i].removeVehicle();
        }
        parkingSpots.clear();
    }
    // Check if the spot is big enough for the vehicle
    virtual boolean canFitInSpot(ParkingSpot spot) = 0;
};

class Bus : public Vehicle {
public:
    Bus() {
        spotsNeeded = 5;
        size = Large;
    }
    // Check if the spot is a Large 
    // Does not check if there are 5 spots.
    bool canFitInSpot(ParkingSpot spot) {
        return spot.getSize() == Large;
    }
};

class Car : public Vehicle {
public:
    Car() {
        spotsNeeded = 1;
        size = Compact;
    }
    // Check if the spot is a Compact or a Large
    bool canFitInSpot(ParkingSpot spot) {
        return spot.getSize() == Large || spot.getSize() == Compact;
    }
};

class Motorcycle : public Vehicle {
public:
    Motorcycle() {
        spotsNeeded = 1;
        size = Motorcycle;
    }
    // Check if the spot is a Motorcycle, a Compact, or a Large
    bool canFitInSpot(ParkingSpot spot) {
        return true;
    }
};
```

The **ParkingSpot** is implemented by having just a variable which represents the size of the spot. We do not need to implement different classes for each size of the spot (e.g. LargeSpot, CompactSpot, and MotorcycleSpot), because the spots do not have different behaviors.

```c
class ParkingSpot {
    Vehicle vehicle;
    VehicleSize spotSize;
    int row;
    int spotNumber;
    Level level;

public:
    ParkingSpot(Level lvl, int r, int n, VehicleSize vs) {
        level = lvl;
        row = r;
        spotNumber = n;
        spotSize = vs;
    }

    bool isAvailable() {
        return vehicle == NULL;
    }

    // Check if the spot is big enough and is available
    // This compares the size only, does not check if it has enough spots
    bool canFitVehicle(Vehicle vehicle) {
        return isAvailable() && vehicle.canFitInSpot(this);
    }

    // Park vehicle in this spot
    // We do this in the parkingspot class because the parkingspot class
    // usually has whether this spot is avaialbe information. 
    bool park(Vehicle v) {
        if (!canFitVehicle(v)) {
            return false;
        }
        vehicle = v;
        vehicle.parkInSpot(this);
        return true;
    }

    int getRow() {
        return row;
    }

    int getSpotNumber() {
        return spotNumber;
    }

    VehicleSize getSize() {
        return spotSize;
    }

    // Remove vehicle from spot
    void removeVehicle() {
        vehicle = NULL;
    }
};
```



