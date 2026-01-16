# route-optimizer
Small router built to call an API service, serve as a stop-gap for appointment assignment on SJ Blinds reps

'''mermaid
flowchart TD
  U[Prospect] --> S1[Step 1: Enter Details\n(name, phone, address, zip)]
  S1 --> S2[Step 2: Combined Calendar\nAny Available times]
  S2 -->|Books Slot| A[Appointment Created\n(assigned by pooled calendar)]
  A --> W[Conversionly Workflow Trigger\nAppt Created/Updated + Confirmed]
  W --> H[Webhook -> Router (Vercel)]
  H -->|Fetch schedules| API1[HighLevel/Conversionly API\nCalendar Events (Rep A/B)]
  H -->|Geocode/Distance| MAPS[Distance calc\n(Google Maps OR zip centroid)]
  H --> D{Pick Winner}
  D -->|Dry Run| L[Log Decision Only]
  D -->|Apply| UPD[Update Appointment assignedUserId\n(+ optional owner updates)]
  UPD --> F1[Existing Rep Workflows\nConfirmation, SMS/Email, Opportunity, Notifications]
'''
