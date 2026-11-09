# Voice Booking Agent — AI Receptionist on Google Calendar

A voice AI receptionist that checks real availability in Google Calendar and books the appointment during the call. The demo is set up for a barbershop, and the same structure works for clinics, beauty salons, hotels, hostels and any other business with a reception.

Try the live demo at [tatulbuilds.dev](https://tatulbuilds.dev/#projects).

## Problem it solves
Small businesses miss bookings when nobody can pick up the phone. This setup answers the caller, offers times that are actually free, and puts the appointment straight into the calendar the staff already use.

## How it works
An [ElevenLabs](https://elevenlabs.io) conversational agent handles the voice call and calls n8n as tools:

1. **[voice-check-availability](../workflows/voice-check-availability.json)** receives a `service` and `date`, reads that day's events, and returns the free slots.
2. **[voice-book-appointment](../workflows/voice-book-appointment.json)** receives `date`, `time`, `service` and `customer_name`, checks the slot again, and creates the calendar event.
3. **[voice-calendar-feed](../workflows/voice-calendar-feed.json)** gives the website the next 7 days of bookings, so visitors can watch theirs appear during the call.
4. **[voice-demo-cleanup](../workflows/voice-demo-cleanup.json)** runs every 15 minutes and deletes demo bookings 60 minutes after they were made.

## Design decisions worth noting
- **Availability is checked twice:** the booking workflow re-checks the slot, so two callers can't take the same time.
- **Rules live in the workflow, not the prompt:** opening hours, durations and closed days are enforced in code, so the agent can't book outside them.
- **Clear failure reasons:** the booking returns `slot_taken`, `outside_hours`, `closed_sunday` and similar, so the agent can respond naturally.
- **The two agent webhooks require an API key header**, so only the agent can call them.

## Setup
- Import the workflows and connect your own Google Calendar account in the calendar nodes.
- Replace `YOUR_CALENDAR_ID` with your calendar's ID. Use the same calendar in all the workflows.
- Create a Header Auth credential (header name `X-API-Key`) for the two agent webhooks.
- Create an ElevenLabs agent and add both webhooks as server tools, sending the same `X-API-Key` header.
- For the website feed, set your own domain in the webhook's allowed origins.

**Only use `voice-demo-cleanup` on a calendar dedicated to the demo. It deletes every event in that calendar once it is 60 minutes old. Replace `YOUR_DEMO_CALENDAR_ID` with that calendar's ID, and leave this workflow out for a real business.**

The feed is public and returns customer names, which suits a demo. For a real business, return only the times.

No credentials are included in these files — add your own after importing.

## Adapting it to another business
Edit the Code nodes in the availability and booking workflows:
- `DURATIONS` holds the services and their lengths.
- The opening hours are `WORK_START` / `WORK_END` in the availability workflow and the `9 * 60` / `18 * 60` check in the booking workflow.
- The closed-day check and the `Europe/Bratislava` time zone, including the `+01:00` offset in the calendar nodes, should match your location.

## Apps used
n8n, ElevenLabs, Google Calendar
