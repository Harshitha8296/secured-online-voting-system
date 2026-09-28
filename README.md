# SecureVote V4

Full Spring Boot academic voting project with actual browser-side face descriptor comparison.

## Key difference from V3
Registration uses face-api.js to detect a face and create a 128-dimensional face descriptor. During voting another live descriptor is generated and Euclidean distance is calculated. Distance <= 0.55 is treated as a match; otherwise the vote is blocked.

## Requirements
JDK 17, IntelliJ IDEA, XAMPP/MySQL, webcam, internet connection for face-api.js and its models.

## Database
Start MySQL in XAMPP and create `online_voting_db` in phpMyAdmin. The app creates tables automatically.

## Run
Run `SecureVoteApplication.java`, then open http://localhost:8081

Admin: admin / admin123

## Test
Register -> capture face -> submit -> Admin login -> Verify voter -> Voter login -> choose nominee -> Verify Face & Vote -> click Vote now. A same-person capture should normally give a smaller distance; a different face should normally exceed the demo threshold.

## Important
This is an academic demonstration, not election-grade biometric security. It has no certified identity proof, robust liveness/anti-spoofing, protected biometric-template architecture, or legal election compliance. The face library/models are loaded from a public CDN; internet is required unless you later host them locally.

## V4.1 vote verification workflow
1. Voter opens the camera and captures a live voting photo.
2. face-api.js compares the live face descriptor with the registered descriptor.
3. If the face matches, the captured voting photo is uploaded to the server.
4. The vote is saved as **PENDING** and is NOT counted yet.
5. Admin Dashboard shows the registered photo and live voting photo side-by-side.
6. Admin can **Approve Vote & Count** or **Reject Vote**.
7. Only an approved vote increments the nominee's vote count and marks the voter as having voted.
