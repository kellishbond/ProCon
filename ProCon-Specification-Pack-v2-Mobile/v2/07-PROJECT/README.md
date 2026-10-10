# ProCon

A Nigeria-first **mobile app (iOS and Android)** connecting customers and businesses with trusted people who can provide digital services, skilled trades and local labour.

## Core Idea
Connect people who need work done with people who can do it.

The marketplace is intentionally broader than a traditional freelance platform.

Examples:
- A business needs a website.
- A family needs a plumber.
- An event needs photographers.
- A homeowner needs painters.
- A company needs cleaners.
- A student needs a tutor.
- Someone needs furniture moved.
- A church needs a keyboard player.
- A business needs a social media manager.

## Documentation
See:
- 01-PRD
- 02-MVP
- 03-UX
- 04-TECHNICAL (includes Mobile-App-Architecture.md)
- 05-ENGINEERING
- 06-AGENT
- 07-PROJECT
- 08-BUSINESS to 16-BACKLOG (Pack 2: business, trust, legal, operations, security, launch, agent context, backlog)
- 00-INDEX-and-Open-Decisions.md and 00-CHANGELOG-Mobile-Pivot.md

## Development Principle
Do not begin by building every possible feature. Validate the core marketplace loop:

Customer posts job → providers discover → provider applies → customer hires → work happens → completion → payment → review.

## Suggested Stack
React Native + Expo (TypeScript), Expo Router, EAS
Node.js + Express
MongoDB
REST API
Realtime messaging
Push notifications (Expo/APNs/FCM)
Paystack/Flutterwave
Cloud storage
Maps/location provider
React + Vite web admin panel
Static website for legal/support pages

## Local Development
Exact commands should be added once the repository is initialized. Expected tools: Node.js, Expo CLI/EAS CLI, Android Studio emulator and/or a physical Android phone, Xcode (Mac) or a physical iPhone with a development build. Use Expo Go only for quick early prototyping.

## Environment
Keep secrets in environment variables or EAS secrets. Never commit .env files containing credentials. Anything bundled in the app (including EXPO_PUBLIC_* values) is public; never put secrets there.

## License
To be determined by the project owner.
