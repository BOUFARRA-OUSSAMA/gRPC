# gRPC Spring Boot Project

This project is a Spring Boot application that uses gRPC for remote procedure calls. It includes a service for managing accounts (`CompteService`), with various operations such as retrieving all accounts, retrieving an account by ID, calculating total balance statistics, saving an account, retrieving accounts by type, and deleting an account.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [gRPC Service](#grpc-service)
- [Protobuf Definitions](#protobuf-definitions)
- [Running the Application](#running-the-application)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

- Java 8 or higher
- Maven 3.6.0 or higher


## Getting Started

1. **Clone the repository**:

    ```sh
    git clone https://github.com/yourusername/grpc2-main.git
    cd grpc2-main
    ```

2. **Build the project**:

    ```sh
    mvn clean install
    ```

3. **Run the application**:

    ```sh
    mvn spring-boot:run
    ```

## gRPC Service

The `CompteService` provides the following operations:

- `AllComptes`: Retrieve all accounts.
- `CompteById`: Retrieve an account by its ID.
- `TotalSolde`: Calculate total balance statistics.
- `SaveCompte`: Save a new account.
- `CompteByType`: Retrieve accounts by type.
- `DeleteCompte`: Delete an account by its ID.

## Protobuf Definitions

The gRPC service and message types are defined in the `compte.proto` file:

```proto
syntax = "proto3";
option java_package = "ma.projet.grpc.stubs";
option java_multiple_files = true;

enum TypeCompte {
  COURANT = 0;
  EPARGNE = 1;
}

message Compte {
  string id = 1;
  float solde = 2;
  string dateCreation = 3;
  TypeCompte type = 4;
}

message CompteRequest {
  float solde = 1;
  string dateCreation = 2;
  TypeCompte type = 3;
}

message SoldeStats {
  int32 count = 1;
  float sum = 2;
  float average = 3;
}

message GetAllComptesRequest {}

message GetAllComptesResponse {
  repeated Compte comptes = 1;
}

message GetCompteByIdRequest {
  string id = 1;
}

message GetCompteByIdResponse {
  Compte compte = 1;
}

message GetTotalSoldeRequest {}

message GetTotalSoldeResponse {
  SoldeStats stats = 1;
}

message SaveCompteRequest {
  CompteRequest compte = 1;
}

message SaveCompteResponse {
  Compte compte = 1;
}

message GetComptesByTypeRequest {
  TypeCompte type = 1;
}

message GetComptesByTypeResponse {
  repeated Compte comptes = 1;
}

message DeleteCompteRequest {
  string id = 1;
}

message DeleteCompteResponse {
  bool success = 1;
}

service CompteService {
  rpc AllComptes(GetAllComptesRequest) returns (GetAllComptesResponse);
  rpc CompteById(GetCompteByIdRequest) returns (GetCompteByIdResponse);
  rpc TotalSolde(GetTotalSoldeRequest) returns (GetTotalSoldeResponse);
  rpc SaveCompte(SaveCompteRequest) returns (SaveCompteResponse);
  rpc CompteByType(GetComptesByTypeRequest) returns (GetComptesByTypeResponse);
  rpc DeleteCompte(DeleteCompteRequest) returns (DeleteCompteResponse);
}


### Running the Application
To run the application, use the following command:

mvn spring-boot:run


This `README.md` file provides a comprehensive overview of your project, including the project structure, getting started instructions, gRPC service details, protobuf definitions, and commands for running and testing the application.