# Pay-slip-Automation-System

This project implements an automated payroll system for ONGC using SAP ABAP. It includes the creation of database tables, setting up a package, and developing the necessary ABAP programs for payroll processing, including pay slip generation.

## Table of Contents

- [Introduction](#introduction)
- [Creating Database Tables](#creating-database-tables)
  - [Table ZPAY](#table-zpay)
  - [Table ZPOS](#table-zpos)
  - [Data Elements](#data-elements)
- [Creating a Package](#creating-a-package)
- [Developing ABAP Programs](#developing-abap-programs)
  - [Program ZAUTO](#program-zauto)
  - [Program ZCALP](#program-zcalp)
- [Screens](#screens)
  - [Input Screen 100](#input-screen-100)
  - [Output Screen 200](#output-screen-200)
- [Creating and Integrating Adobe Forms](#creating-and-integrating-adobe-forms)
  - [Adobe Form Interface ZHR_PAYROLL_PDF](#adobe-form-interface-zhr_payroll_pdf)
  - [Adobe Form ZHR_PAYROLL_PDF](#adobe-form-zhr_payroll_pdf)
- [Running the Payroll Automation System](#running-the-payroll-automation-system)

## Introduction

We will cover the detailed implementation of the ONGC Pay Slip Automation System using SAP ABAP in this project. This includes creating database tables, setting up a package, and developing the required ABAP programs.

## Creating Database Tables

### Table ZPAY

The `ZPAY` table contains all the details about the employees required for payroll processing.

**Steps:**
1. Navigate to SE11 (ABAP Dictionary).
2. Enter the table name `ZPAY` and click on the "Create" button.
3. Define the table fields:

   | Field       | Data Type | Length | Description               |
   |-------------|------------|--------|---------------------------|
   | MANDT       | CLNT       | 3      | Client                    |
   | CPFNO       | INT4       | 10     | Employee CPF Number       |
   | NAME        | CHAR       | 25     | Employee Name             |
   | EMP_POS     | CHAR       | 2      | Employee Position         |
   | PAYRATE     | INT4       | 10     | Employee Basic Pay Rate   |
   | PAN         | CHAR       | 10     | PAN Number                |
   | DOB         | DATS       | 8      | Date of Birth             |
   | DOJ         | DATS       | 8      | Date of Joining           |
   | DOLP        | DATS       | 8      | Date of Leaving Payroll   |
   | BANK_ACC_NO | INT8       | 19     | Bank Account Number       |

4. Set the Delivery Class to A (Application table).
5. Data Browser should be on Display/Maintenance Allowed.
6. Set the Enhancement Category to “Can Be Enhanced (Deep)”.

Activate the table and resolve any errors that may appear in the Activation Log.

### Table ZPOS

The `ZPOS` table stores details related to employee positions and payroll information.

**Steps:**
1. Navigate to SE11 (ABAP Dictionary).
2. Enter the table name `ZPOS` and click on the "Create" button.
3. Define the table fields:

   | Field         | Data Type | Length | Description                |
   |---------------|------------|--------|----------------------------|
   | MANDT         | CLNT       | 3      | Client                     |
   | EMP_POS       | CHAR       | 2      | Position                   |
   | DESIGNATION   | CHAR       | 25     | Designation                |
   | PAYSCALE_LOW  | INT4       | 10     | Payscale Low               |
   | PAYSCALE_HIGH | INT4       | 10     | Payscale High              |

Activate the table.

### Data Elements

Data elements in SAP define the type of a table field or structure component, describing semantic attributes like data type, length, and associated domain or search help.

**Creating a Data Element:**
1. Navigate to SE11 and select the "Data type" radio button.
2. Enter the name `ZCPFNO` and click "Create".
3. In the pop-up window, select "Data Element" and click the green checkmark.
4. Enter the short description: `CPF Number`.
5. Assign Domain `NUM10` (or create a new one if it does not exist).
6. Define Field Labels and activate the data element.

## Creating a Package

**Steps to create package `ZAUTOPAY`:**
1. Navigate to SE80 (Object Navigator).
2. Right-click on "Repository Browser" and select "Create > Package".
3. Enter the package name `ZAUTOPAYROLL` and description.
4. Save and activate the package.

## Developing ABAP Programs

### Program ZAUTO

The `ZAUTO` program automates various payroll-related tasks.

**Steps:**
1. Navigate to SE38 (ABAP Editor).
2. Enter the program name `ZAUTO` and click on the "Create" button.
3. Enter the title and type as "Executable Program".
4. Include necessary subprograms: `ZAUTOF01`, `ZAUTOI01`, `ZAUTOO01`, `ZAUTOTOP`.
5. Write ABAP code to perform payroll automation tasks using tables `ZPAY` and `ZPOS`.
6. Create a transaction code `ZAUTOPR` for the program.
7. Save, check, and activate the program.

### Program ZCALP

The `ZCALP` program is used for payslip generation.

**Steps:**
1. Navigate to SE38 (ABAP Editor).
2. Enter the program name `ZCALP` and click on the "Create" button.
3. Enter the title and type as "Executable Program".
4. Include necessary subprograms: `ZCALPF01`, `ZCALPI01`, `ZCALPO01`, `ZCALPTOP`.
5. Write ABAP code to calculate earnings, deductions, and net income using basic pay from the program `ZAUTO`.
6. Generate the payslip using an Adobe form.
7. Save, check, and activate the program.

## Screens

### Input Screen 100

Screen 100 is used for inputting parameters like the employee CPF number (`pcpf`) and month (`pmon`) for payslip generation.

**Steps:**
1. Navigate to SE51 (Screen Painter).
2. Enter the program name `ZCALP` and screen number `0100`. Click on "Create".
3. Define the screen attributes and layout:
   - Add input fields for `pcpf` and `pmon`.
   - Add text labels and a "Submit" pushbutton.
4. Define Flow Logic for PBO and PAI.

### Output Screen 200

Screen 200 displays payslip details in a table format using an Adobe form.

**Steps:**
1. Navigate to SE51 (Screen Painter).
2. Enter the program name `ZCALP` and screen number `0200`. Click on "Create".
3. Define the screen attributes and layout:
   - Add a custom container for the Adobe form.
   - Add any necessary UI elements like buttons for navigation or print options.

## Creating and Integrating Adobe Forms

### Adobe Form Interface ZHR_PAYROLL_PDF

**Steps:**
1. Navigate to SFP (Form Builder).
2. Create a new interface `ZHR_PAYROLL_PDF`.
3. Define import parameters and tables for the form.

### Adobe Form ZHR_PAYROLL_PDF

**Steps:**
1. Navigate to SFP (Form Builder).
2. Create a new form `ZHR_PAYROLL_PDF` and link it to the interface.
3. Use Adobe LiveCycle Designer to design the form layout:
   - Add text fields and bind them to corresponding data fields.
   - Create a table for detailed payslip information.

## Running the Payroll Automation System

**Steps:**
1. Navigate to SE38 (ABAP Editor).
2. Execute the `ZAUTO` program for automation tasks.
3. Execute the `ZCALP` program to generate the payslip:
   - Input the CPF number and month on screen 100.
   - Submit to process and navigate to screen 200.
   - Review the payslip details displayed in the Adobe form.
