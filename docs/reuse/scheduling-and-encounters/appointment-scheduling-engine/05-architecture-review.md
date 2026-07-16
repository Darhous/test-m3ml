# Architecture Review — Appointment Scheduling Engine

Cal.com's slot/availability/booking model directly fits Wave 3's
"Scheduling" and "Resource slots" capabilities; its workflow-automation
feature (no-show reduction, reminders) composes with Novu (Module 5)
rather than requiring Cal.com's own notification stack — avoiding
running two notification systems.
