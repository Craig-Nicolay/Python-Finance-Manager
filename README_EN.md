# Python Finance Manager

[![Support Python versions](https://img.shields.io/pypi/pyversions/pdfplumber.svg)](https://pypi.python.org/pypi/pdfplumber)

[Deutsche Version](README.md)

**Python Finance Manager for Financial Overview from comdirect Financial Reports**<br>
Using a Python script, the PDF financial reports stored on the PC for a given year are read, and the included income and expenses are assigned to booking groups based on keywords.
The result is CSV files with balances and transactions per group name, which can then be further analyzed in Excel, for example.

## Disclaimer

**This is purely a hobby project.**
**There is no guarantee for error-free operation, support, or timely assistance!**
**The mentioned product and brand names are the property of their respective owners.**

## Requirements

- Python 3.7+

Download and support for the Python runtime environment can be found on the [support page](https://www.python.org/).
The Python library [pdfplumber](https://github.com/jsvine/pdfplumber) is required to read the PDF financial reports.

## Installation

1. Download [Python 3.11+](https://www.python.org/)
2. On Windows: Open the command line window (Start by pressing the "Windows key" + "R". Then enter "cmd.exe" and confirm with "Enter").
   All further steps are to be executed in the command line window.
3. Check the Python version with the command: python --version
4. Update Python with the command: pip install update
5. Install pdfplumber: pip install pdfplumber
6. Download [com_fm.py](com_fm.py) and [com_fm.ini](com_fm.ini)
7. Adjust the parameters in com_fm.ini, see below

## Configuration

The file [com_fm.ini](com_fm.ini) contains all the necessary parameters for individual customization:

| Parameter | Description |
|-------------------------------------------------------|------------------------------------------------------------------|
| path : D:\\comdirect\\Kto1234567 | Path to the location where comdirect financial reports are stored. |
| year : 2022 | Analysis year |
| Group name : Keyword1, Keyword2,... e.g.:<br>Online Expenses : paypal,amazon,internet,online | All income and expenses whose text contains one of the following keywords will be summarized under the group name. |

com_fm.ini already contains example group names and keywords, which can be individually expanded or customized. Note: The separation between path, year, and group names is " : " (a space before and after the colon). The keywords (written in lowercase) are separated by commas without spaces.
com_fm.ini is searched in the order of entry. Note that very short keywords can suppress later longer keywords. For example, the keyword "markt" can prevent the keyword "kaufmarkt" from being found.

## Structure of the Financial Reports

The relevant transactions for evaluation begin on page 2 of the financial report and start with reading the Old Balance. Further income and expenses are read line by line until the New Balance is reached. The booking text lines are taken into account, e.g.: 02.06.2022 Direct Debit/ CITY SERVICES KD.-NR.345,00-INSTALLMENT0 -91,00<br>
The text is compared with the keywords stored in com_fm.ini, and the booking amount is assigned to the group balance. The text is converted to lowercase during comparison so that case sensitivity does not matter. If no assignment can be found, income will be assigned to the group "Miscellaneous Income" and expenses to the group "Miscellaneous Expenses".
To verify and possibly supplement keywords in com_fm.ini, all bookings of the groups "Miscellaneous Income" and "Miscellaneous Expenses" are output at the end. If com_fm.ini does not contain any group names, all income will be assigned to "Miscellaneous Income" and expenses to "Miscellaneous Expenses".

## Execution

com_fm.py and com_fm.ini must be in the same directory.<br>

```sh
python com_fm.py
```
Runtime output:
```sh
Finanzreport_Nr._01_per_03.02.2020.pdf saldo delta 0.0
Finanzreport_Nr._02_per_02.03.2020.pdf saldo delta 0.0
...
```
During processing, the names of the financial report files being read are displayed. A balance discrepancy is shown as delta in case of an analysis error.

## Result Files

Two CSV files are generated: year_finmnanager.csv and year_finmnanager_bookings.csv. year_finmnanager.csv contains the group overview and group balances with the columns: Year; Group name; Number of transactions in the group; Balance.
year_finmnanager_bookings.csv contains Booking date; Group name; Transaction; Booking text; Amount.

## License

**Creative Commons BY-NC-SA**<br>
Give Credit, NonCommercial, ShareAlike

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.


[comment]: # (:large_blue_circle:)