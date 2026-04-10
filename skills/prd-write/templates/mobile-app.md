# Template: Mobile App Feature PRD

Use this as a starting point for mobile app features.

Typical sections to emphasize:
- **Platform**: iOS, Android, or both? React Native / Flutter / native?
- **Offline support**: Does this work without connectivity?
- **Push notifications**: Are notifications part of this feature?
- **App Store impact**: Does this require App Store review or new permissions?
- **Device considerations**: Camera, GPS, biometrics, etc.?

## Mobile-Specific User Stories to Consider

- As a **mobile user on slow connection**, I want to **[complete core actions with degraded but usable experience]**, so that **[I'm not blocked by connectivity]**. Because otherwise **[I abandon the flow before completion]**.
- As a **user granting permissions**, I want to **[understand why access is needed]**, so that **[I feel safe approving]**. Because otherwise **[I deny permissions and key flows fail]**.
- As a **user receiving notifications**, I want to **[control frequency and type]**, so that **[I'm not overwhelmed]**. Because otherwise **[I mute notifications or uninstall the app]**.

## Mobile-Specific Success Metrics to Consider

- Daily active users (DAU) for the feature
- Feature flow crash-free rate target (define baseline + target window, e.g., 7/30 days post-release)
- App store rating impact (monitor after release)
- Session depth (how many steps users complete in the flow)
- Permission grant rate (if permissions are requested)
