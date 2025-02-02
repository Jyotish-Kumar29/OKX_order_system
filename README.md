# OKX Order System

## Overview

**OKX Order System** is a C++ application that interacts with the OKX cryptocurrency trading platform. The application allows users to perform various trading operations, including placing orders, modifying orders, cancelling orders, and retrieving order history.

## Features

- **Place Orders:** Allows placing market and limit orders on the OKX platform.
- **Modify Orders:** Modify existing orders, such as changing the quantity or price.
- **Cancel Orders:** Cancel open orders by order ID.
- **View Order History:** Retrieve and display the history of executed orders.
- **View Open Orders:** Retrieve and display open (active) orders.

## Prerequisites

- **C++ Compiler:** C++17 or later.
- **CMake:** Version 3.10 or later.
- **Visual Studio 2022:** (or another C++ IDE)
- **vcpkg:** A package manager for C++ libraries.

## Dependencies

- **cURL:** For making HTTP requests.
- **OpenSSL:** For handling secure connections (HTTPS).
- **nlohmann/json:** For parsing JSON responses.
- **dotenv:** For loading environment variables from a `.env` file.

## Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/Jyotish-Kumar29/OKX_Order_System.git
cd OKXOrderSystem
```

### Step 2: Install Dependencies

1. Install `vcpkg` (if not already installed):
   ```bash
   git clone https://github.com/microsoft/vcpkg.git
   cd vcpkg
   .\bootstrap-vcpkg.bat
   ```

2. Install required packages using `vcpkg`:
   ```bash
   .\vcpkg install curl openssl nlohmann-json
   ```

### Step 3: Set Up Environment Variables

Create a `.env` file in the project root directory with the following content:

```plaintext
API_KEY=your_api_key
SECRET_KEY=your_secret_key
PASSPHRASE=your_passphrase
```

Replace `your_api_key`, `your_secret_key`, and `your_passphrase` with your actual OKX API credentials.

### Step 4: Configure CMake

Create a `CMakeLists.txt` file with the following content:

```cmake
cmake_minimum_required(VERSION 3.10)
project(OKXOrderSystem)

set(CMAKE_CXX_STANDARD 17)

# Set VCPKG
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake)
set(VCPKG_TARGET_TRIPLET "x64-windows")

# Find required packages
find_package(CURL REQUIRED)
find_package(OpenSSL REQUIRED)
find_package(nlohmann_json REQUIRED)

# Include directories
include_directories(${CURL_INCLUDE_DIRS} ${OPENSSL_INCLUDE_DIRS})

# Add executable
add_executable(okx_order_system main.cpp okx_client.cpp)

# Link libraries
target_link_libraries(okx_order_system ${CURL_LIBRARIES} ${OPENSSL_LIBRARIES} nlohmann_json::nlohmann_json)
```

### Step 5: Build the Project

1. Open the project folder in Visual Studio 2022.
2. Open **CMakeLists.txt** in Visual Studio.
3. Right-click on the **CMakeLists.txt** file in the Solution Explorer and choose **Build**.

### Step 6: Run the Project

Run the `okx_order_system` executable generated by the build process.

## Usage

### Example Commands

- **Place an Order**
  ```cpp
  client.placeOrder("MAGIC-USDT-SWAP", "buy", "limit", 1, 0.3);  // works for open order
  client.placeOrder("MAGIC-USDT-SWAP", "buy", "limit", 1, 0.345); // works for filled order
  ```

- **Get Pending Orders**
  ```cpp
  client.getPendingOrders("limit", "SWAP"); // works
  ```

- **Get Order History**
  ```cpp
  client.getOrderHistory("MAGIC-USDT-SWAP", "SWAP"); // works
  ```

- **Cancel an Order**
  ```cpp
  client.cancelOrder("MAGIC-USDT-SWAP", "1702742015357800448"); // works
  ```

- **Get Open Orders**
  ```cpp
  client.getOpenOrders("MAGIC-USDT-SWAP", "SWAP"); // works
  ```

- **Modify an Order**
  ```cpp
  client.modifyOrder("1703908579612348416", "MAGIC-USDT-SWAP", "2", "0.352"); // works
  ```

- **Get Order Book**
  ```cpp
  std::cout << client.getOrderBook("MAGIC-USDT-SWAP") << std::endl;
  ```

- **Get Current Positions**
  ```cpp
  std::cout << client.getCurrentPositions() << std::endl;
  ```

## Environment Variables

- **API_KEY:** Your OKX API key.
- **SECRET_KEY:** Your OKX API secret key.
- **PASSPHRASE:** Your OKX API passphrase.

## Error Handling

The application checks for API response codes and handles errors such as order cancellations, order modifications, and general API failures. Errors are printed to the console with appropriate messages.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

