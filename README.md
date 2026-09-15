# Python-Network-Programming
Python Network Programming project that demonstrates HTTP client-server communication, JSON data exchange, and email protocols. The project simulates an airline system for managing pre-departure and in-flight information, while also demonstrating SMTP, POP3, and IMAP communication and automated safety alerts.
# Python Network Programming – Airline Communication System

## Project Overview

This project was developed as part of the **ITPNA2-12 Python Network Programming** module at Eduvos. The project demonstrates the use of Python for network communication by simulating an airline system that monitors aircraft activities before departure and during flight.

The project focuses on communication between **clients and servers**, exchanging information using **HTTP and JSON**, and working with common email protocols such as **SMTP, POP3, and IMAP**.

The scenario is based on an airline called **Aero Airlines**, which operates flights between different cities in South Africa. The system monitors important aircraft information such as aircraft status, passenger boarding, fueling, door state, pushback time, autopilot status, cabin pressure, and Wi-Fi usage.

The programs were designed using beginner-friendly Python concepts while demonstrating practical networking principles.

---

## Project Objectives

The main objectives of this project are to:

* Demonstrate basic Python network programming.
* Create an HTTP server that provides information to clients.
* Use JSON to exchange structured information between applications.
* Create client applications that communicate with HTTP servers.
* Allow staff applications to update aircraft information using HTTP requests.
* Monitor and update in-flight information periodically.
* Demonstrate the differences between SMTP, POP3, and IMAP.
* Use Python to send and retrieve emails.
* Monitor aircraft information and generate an email alert when a safety condition is outside the required margin.

---

## Technologies and Python Modules

The project uses Python and several built-in or commonly used networking modules.

### Python

Python is the main programming language used throughout the project. Basic concepts such as:

* Variables
* Dictionaries
* Functions
* Classes
* Loops
* Conditional statements
* File handling
* Exception handling

are used to implement the different applications.

### HTTP

HTTP is used for communication between the client applications and the server.

The Python `http.server` module is used to create a simple HTTP server capable of receiving requests and sending responses.

### JSON

JSON (JavaScript Object Notation) is used to represent aircraft information in a structured format.

For example:

```json
{
    "Aircraft Status": "Ready for departure",
    "Passenger Boarding Number": "128",
    "Fueling": "Completed",
    "Door State": "Closed",
    "Push Back Time": "13:45"
}
```

Python's `json` module is used to convert Python dictionaries into JSON data and to read JSON data received from clients or files.

### Requests

The `requests` library is used by client applications to make HTTP requests to the server.

For example:

```python
response = requests.get("http://localhost:8080")
```

and:

```python
response = requests.post("http://localhost:8081", json=data)
```

### SMTP

The `smtplib` module is used to demonstrate sending email messages from Python.

SMTP is primarily used for sending email.

### POP3

The `poplib` module is used to demonstrate retrieving email messages using POP3.

POP3 generally downloads messages from a mail server to a client.

### IMAP

The `imaplib` module is used to demonstrate accessing emails stored on a mail server.

IMAP is particularly useful when emails need to remain on the server and be accessed from multiple devices.

---

# Project Structure

The project contains several Python programs and data files.

```text
Python-Network-Programming/
│
├── pre_departure.txt
├── in_flight.txt
│
├── pre_departure_server.py
├── client_pre_departure.py
│
├── pre_departure_server_post.py
├── update_pre_departure.py
│
├── inflight_server.py
├── inflight_update.py
│
├── send_email.py
├── pop3_client.py
├── imap_client.py
│
└── safety_monitor.py
```

The exact files can be organised differently depending on how the project is submitted.

---

# Section 1 – Pre-Departure Information

The first part of the project focuses on information collected while an aircraft is still on the ground.

The information includes:

* Aircraft status
* Passenger boarding number
* Fueling status
* Door state
* Pushback time

The information can initially be stored in a text file such as:

```text
Aircraft Status: Ready for departure
Passenger Boarding Number: 128
Fueling: Completed
Door State: Closed
Push Back Time: 13:45
```

The server reads this information and converts it into structured JSON data.

---

# Section 1.1 – HTTP JSON Server

The `pre_departure_server.py` program creates a basic HTTP server.

The server listens on:

```text
http://localhost:8080
```

When a client sends a GET request, the server:

1. Opens the pre-departure information file.
2. Reads the information.
3. Places the information into a Python dictionary.
4. Converts the dictionary into JSON.
5. Sends the JSON response to the client.

This demonstrates the basic client-server model.

```text
             GET Request
Client ----------------------> HTTP Server
                                |
                                | Reads file
                                | Converts data
                                | to JSON
                                |
Client <---------------------- Server
             JSON Response
```

---

# Section 1.2 – Pre-Departure Client

The `client_pre_departure.py` program acts as an HTTP client.

It connects to:

```text
http://localhost:8080
```

The client sends a GET request and receives the aircraft information from the server.

The JSON response is then converted into Python data and displayed to the user.

This demonstrates how a client application can request information from a server.

---

# Section 1.3 – Updating Pre-Departure Information

The project also includes an HTTP POST system that allows staff at the gate to update aircraft information.

The staff client sends information to the server using a POST request.

For example:

```python
data = {
    "Aircraft Status": "Ready",
    "Passenger Boarding Number": "130",
    "Fueling": "In progress",
    "Door State": "Open",
    "Push Back Time": "14:00"
}
```

The server receives the JSON information and updates the stored aircraft information.

The communication can be represented as:

```text
Gate Staff Application
          |
          | HTTP POST + JSON
          v
     HTTP Server
          |
          | Update
          v
 Aircraft Information
```

This demonstrates how HTTP can be used not only to retrieve information but also to send information to a server.

---

# Section 1.4 – In-Flight Events

The project also monitors information while the aircraft is in flight.

The monitored information includes:

* Autopilot status
* Cabin pressure
* Wi-Fi usage

Example:

```text
Autopilot Status: ON
Cabin Pressure: Normal
Wi-Fi Usage: Medium
```

An HTTP server provides this information to clients in JSON format.

The client can request the current information from the server and display it.

---

# Section 1.5 – Automatic Updates

The `inflight_update.py` program demonstrates periodic updates of in-flight information.

The program uses Python's `time` module and updates the information every **5 seconds**.

For example:

```python
time.sleep(5)
```

This demonstrates a simple way of creating a program that performs an operation repeatedly after a specified period.

---

# Section 2 – Email Activities

The second section focuses on email communication and the three major email protocols covered in the project:

* SMTP
* POP3
* IMAP

These protocols have different purposes.

## SMTP

SMTP is mainly used for **sending email**.

The Python `smtplib` module can be used to connect to an SMTP server and send a message.

## POP3

POP3 is used for **receiving email**.

The Python `poplib` module can connect to a POP3 server and retrieve messages.

POP3 commonly downloads messages from the server, making it less suitable when the same mailbox needs to stay synchronised across multiple devices.

## IMAP

IMAP is also used for **receiving email**, but it normally keeps messages stored on the mail server.

This makes IMAP more suitable for users who access their mailbox from multiple devices.

---

# Section 2.1 – Email Protocol Comparison

| Protocol | Main Purpose    | Python Module | Mail Storage                                 |
| -------- | --------------- | ------------- | -------------------------------------------- |
| SMTP     | Sending email   | `smtplib`     | Sends mail between clients/servers           |
| POP3     | Receiving email | `poplib`      | Usually downloads mail to the client         |
| IMAP     | Receiving email | `imaplib`     | Keeps mail on the server and synchronises it |

---

# Section 2.2 – Email Programs

The project demonstrates simple Python programs for working with SMTP, POP3, and IMAP.

### SMTP Program

The SMTP program creates an email message and sends it through an SMTP server.

### POP3 Program

The POP3 program connects to a POP3 server, retrieves messages, displays subjects, and demonstrates how an email can be deleted.

### IMAP Program

The IMAP program connects securely to an IMAP server, searches for unread emails, displays their subjects and bodies, and marks the messages as read.

The IMAP implementation is particularly relevant to the scenario because the helpdesk needs to process unread support emails without repeatedly processing the same messages.

---

# Section 3 – Aviation Safety Monitoring

The final section combines networking concepts with email communication.

The program monitors in-flight information and checks whether the information is within the expected safety conditions.

For example, the program can check:

```text
Cabin Pressure: Normal
```

If the cabin pressure is not normal, the program identifies the condition as a potential safety problem.

The system can then send an email notification to the monitoring service.

The basic process is:

```text
In-Flight Information
          |
          v
    Safety Monitor
          |
          v
   Check Conditions
       /       \
    Safe       Unsafe
     |            |
     v            v
 Continue      Send Email
 Monitoring     Alert
```

This demonstrates how Python network programming can be used to monitor information and communicate an alert when a condition requires attention.

---

# Security Considerations

The email portion of the project avoids placing passwords directly inside the Python source code.

Instead, the password can be requested when the program runs.

For example:

```python
from getpass import getpass

password = getpass("Enter your password: ")
```

Using `getpass` prevents the password from being displayed normally while it is being entered.

For a real-world system, additional security measures would be required, especially because aviation systems and email credentials are sensitive.

---

# How to Run the Project

## 1. Install Python

Make sure Python is installed on the computer.

Check the installation using:

```bash
python --version
```

---

## 2. Install Requests

Some of the client programs use the `requests` library.

Install it using:

```bash
pip install requests
```

---

## 3. Start the HTTP Server

Open a terminal in the project folder and run:

```bash
python pre_departure_server.py
```

The terminal should display something similar to:

```text
Server running on http://localhost:8080
```

Keep this terminal open because the server needs to continue running.

---

## 4. Run the Client

Open another terminal in the same project folder and run:

```bash
python client_pre_departure.py
```

The client should connect to the server and display the pre-departure information.

---

## 5. Test the POST Application

Start the POST server:

```bash
python pre_departure_server_post.py
```

Then, from another terminal, run:

```bash
python update_pre_departure.py
```

The client sends the updated information to the server.

---

## 6. Test the In-Flight Server

Start the in-flight server:

```bash
python inflight_server.py
```

Then run the corresponding client application to retrieve the current in-flight information.

The update program can also be started:

```bash
python inflight_update.py
```

It will update the information every five seconds.

---

# Learning Outcomes

This project helped demonstrate several important Python networking concepts, including:

* Creating basic HTTP servers.
* Creating HTTP clients.
* Sending GET requests.
* Sending POST requests.
* Working with JSON data.
* Reading and writing files.
* Using Python dictionaries to represent structured data.
* Using loops and conditional statements.
* Creating programs that run at regular intervals.
* Sending emails using SMTP.
* Receiving emails using POP3 and IMAP.
* Processing unread emails.
* Working with email subjects and message bodies.
* Creating a basic monitoring and alert system.

---

# Reference

The networking concepts used in this project were studied with reference to:

**Rhodes, B. and Goerzen, J. (2010). *Foundations of Python Network Programming: The Comprehensive Guide to Building Network Applications with Python*. 2nd Edition. Apress.**

The book was used as a reference for understanding Python network programming concepts, including client-server communication and network protocols.

---

# Disclaimer

This project is an educational simulation created for the Python Network Programming module. It does not represent a real aviation control or aircraft monitoring system.

Real aviation systems require specialised hardware, highly secure communication protocols, redundancy, certification, and strict safety standards.
