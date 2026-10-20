# GrabPic

GrabPic helps people find their own photos in large event albums. An organizer uploads the event's photos to a private album and shares one link. A guest takes a selfie, and GrabPic returns every photo where that face appears, so nobody has to scroll through thousands of images.

This project is currently in development.

## Features

**For guests**
- Take a selfie with the front camera or upload a photo
- View all matching photos from an event
- Download individual photos or the full set
- Delete your selfie and face data at any time

**For organizers**
- Create an event and upload photos in batches
- Track how each photo is being processed
- Share a single guest link
- Choose how long face data is kept after the event
- Require guests to opt in before they are matched
- Delete an event and all of its data

## How it works

When an organizer uploads photos, the files go directly to cloud storage. A background worker then detects faces in each photo and converts every face into a numeric embedding, which is stored in MongoDB. When a guest uploads a selfie, GrabPic converts it into the same kind of embedding and searches for the closest matches within that event.

## Privacy and consent

Face data is sensitive, so consent and deletion are built into the design:

- Guests must opt in before their selfie is compared with event photos.
- Face data is deleted automatically after the retention period the organizer chooses.
- Guests can delete their selfie and matches at any time.
- Organizers see processing status and photos, but never guests' face data.
- Selfies are converted to an embedding and not stored as images, unless the guest chooses to keep them.

## Tech stack

- **Frontend:** React, with light and dark themes
- **Backend:** Node.js and Express
- **Database:** MongoDB, with Atlas Vector Search for face matching
- **Background jobs:** BullMQ and Redis
- **File storage:** Amazon S3
- **Face detection:** face-api.js
