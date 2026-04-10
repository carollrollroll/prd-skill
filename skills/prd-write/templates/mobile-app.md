# Template: Mobile App Feature PRD

Use this as a starting point for mobile app features.

Typical sections to emphasize:
- **Platform**: iOS, Android, or both? React Native / Flutter / native?
- **Offline support**: Does this work without connectivity?
- **Push notifications**: Are notifications part of this feature?
- **App Store impact**: Does this require App Store review or new permissions?
- **Device considerations**: Camera, GPS, biometrics, etc.?

## Mobile-Specific User Stories to Consider

- As a **mobile user on slow connection**, I want to [action], so that [I'm not blocked by connectivity]
- As a **user granting permissions**, I want to [understand why], so that [I feel safe approving]
- As a **user receiving notifications**, I want to [control frequency], so that [I'm not overwhelmed]

## Mobile-Specific Success Metrics to Consider

- Daily active users (DAU) for the feature
- Crash rate < 0.1% of sessions
- App store rating impact (monitor after release)
- Session depth (how many steps users complete in the flow)
- Permission grant rate (if permissions are requested)
