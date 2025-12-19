Project: Tours & Travels CRM
Technical Component: BookingTriggerHandler

Executive Summary
The Tours & Travels CRM was developed to solve operational inefficiencies in the travel industry, such as manual booking tracking and inconsistent customer communication. This project implements a full booking lifecycle—from inquiry to feedback—using a mix of declarative (no-code) and programmatic (Apex) Salesforce tools.

Project Data Model
The system is built on seven custom objects linked to ensure data integrity:

Customer_info__c: Centralized customer data.

Booking__c: The parent object for all trip details.

BookingGuest__c: Child records for each traveler.

BookingPayment__c: Automated tracking of financial status.

TravelPackage__c: Catalog of global tour packages.

Employee__c & Feedback__c: Management of tour guides and customer satisfaction.

Programmatic Logic: BookingTriggerHandler
The core of the automation is found in the BookingTriggerHandler class, which is triggered during the after insert and after update phases of a Booking__c record.

Key Methods:
createPaymentRecords: When a booking is inserted, this method automatically generates a BookingPayment__c record with a default status of "Pending" and sets the payment date to the current day.
createBookingGuests: This method reads the Number_of_Travelers__c from the booking and uses a loop to create the corresponding number of BookingGuest__c records automatically.
BookingConfirmationEmailer (Asynchronous): Uses a @future method to send confirmation emails once a booking is confirmed to ensure a smooth user experience.

Key Automations & Security
Approval Process: Cancelled bookings are automatically locked and sent to a manager for approval before the status is finalized.
Validation Rules: Ensures data quality by enforcing 10-digit phone numbers and preventing future dates for a customer's Date of Birth.
Security Model: Implemented a hierarchy where CEOs have full visibility, while Tour Guides only see their assigned customers through Sharing Rules.
Dynamic Forms: Cancellation fields on the Booking record remain hidden until the status is changed to "Cancelled".
Deployment & Testing
Testing: Achieved 90%+ code coverage with the BookingTriggerTest class, which validates that payments and guests are created correctly.
Data Migration: Successfully imported over 20 records for each major object using the Salesforce Data Import Wizard.



Deployment: Managed via Change Sets, packaging all metadata, code, and security configurations for a safe production release.
