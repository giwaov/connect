# Stacks Authentication Example

## Overview
This example shows how to authenticate users with the Stacks blockchain.

## Setup
```bash
npm install @stacks/connect
```

## Authentication Flow
```javascript
import { AppConfig, UserSession, showConnect } from '@stacks/connect';

const appConfig = new AppConfig(['store_write']);
const userSession = new UserSession({ appConfig });

function authenticate() {
  showConnect({
    appDetails: {
      name: 'My Stacks App',
      icon: window.location.origin + '/icon.png',
    },
    redirectTo: '/',
    onFinish: () => {
      const userData = userSession.loadUserData();
      console.log('User address:', userData.profile.stxAddress);
    },
    userSession,
  });
}
```

## Check Auth Status
```javascript
if (userSession.isSignInPending()) {
  userSession.handlePendingSignIn().then(userData => {
    console.log('Signed in:', userData);
  });
} else if (userSession.isUserSignedIn()) {
  const userData = userSession.loadUserData();
  console.log('Already signed in:', userData.profile.stxAddress);
}
```
