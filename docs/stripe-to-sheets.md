# Stripe → Google Sheets

## Problem it solves
A business taking payments through Stripe wants every successful payment recorded in a spreadsheet automatically, so the finance team doesn't have to copy data by hand.

## How it works
1. **Stripe Trigger** fires whenever a payment succeeds.
2. The payment details (amount, customer, date) are passed to the next node.
3. **Google Sheets** appends a new row with that data.

## Setup
- Connect your Stripe account in the Stripe Trigger node.
- Connect your Google account in the Google Sheets node.
- Replace `YOUR_SHEET_ID` with your spreadsheet's ID.

## Notes
This is a starter template. In a real build I'd add error handling and format the amount from cents to dollars.
