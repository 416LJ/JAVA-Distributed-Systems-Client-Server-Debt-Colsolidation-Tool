# Distributed Systems Client-Server Debt Consolidation Tool

A Java-based microservice application that demonstrates a client-server architecture using Java RMI (Remote Method Invocation). This tool provides services for loan payment calculation, social insurance number (SIN) validation, and simple arithmetic operations.

## Features

- **Interest Calculator**: Calculate monthly and total payments for a loan based on annual interest rate, number of years, and loan amount.
- **SIN Validator**: Validate Canadian Social Insurance Numbers checking length, range, and checksum using the Luhn algorithm.
- **Simple Calculator**: Perform basic arithmetic operations remotely.

## Project Structure

The project is structured as a standard Java application:

- `src/main/java/com/interestcalculator/client`: Client-side application and Command Line Interface (CLI).
- `src/main/java/com/interestcalculator/server`: Server-side implementation, RMI registry setup, and service binding.
- `src/main/java/com/interestcalculator/service`: Definition of the remote service interface (`InterestCalculatorService`).
- `src/main/java/com/interestcalculator/core`: Core business logic classes (`PaymentPlan`, `SocialInsuranceNumber`).
- `src/main/java/com/interestcalculator/shared`: Shared utilities.

## Prerequisites

- Java Development Kit (JDK) 8 or higher.

## Usage

### 1. Compile the Project

Navigate to the project root directory and compile the Java files. We'll output the class files to a `bin` directory (create it if it doesn't exist).

```bash
mkdir -p bin
javac -d bin src/main/java/com/interestcalculator/client/*.java \
src/main/java/com/interestcalculator/server/*.java \
src/main/java/com/interestcalculator/service/*.java \
src/main/java/com/interestcalculator/core/*.java \
src/main/java/com/interestcalculator/shared/*.java
```

### 2. Start the RMI Registry

The RMI registry must be running for the server to register its services. Run this from the `bin` directory.

```bash
cd bin
rmiregistry
```

_Note: Keep this terminal window open. In some environments, you may need to run this in the background or use `start rmiregistry` on Windows._

### 3. Start the Server

Open a new terminal, navigate to the `bin` directory, and start the server.

```bash
cd bin
java com.interestcalculator.server.Main
```

You should see a message indicating the RMI registry is running on port 1099.

### 4. Start the Client

Open a third terminal, navigate to the `bin` directory, and start the client application.

```bash
cd bin
java com.interestcalculator.client.Main
```

Follow the on-screen prompts to use the application.

## Key Components

### Social Insurance Number (SIN) Validation

Located in `com.interestcalculator.core.SocialInsuranceNumber`, this static utility verifies SINs. It checks:

- Length (9 digits) and numeric range.
- Checksum validation using the Luhn algorithm.

### Loan Payment Calculation

The `InterestCalculatorServiceImpl` allows clients to compute payment plans remotely, returning a `PaymentPlan` object containing monthly and total payment details.

### Simple Calculator

Performs basic arithmetic operations via the `SimpleCalculator` class, exposed through the RMI service.
