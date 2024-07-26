This repository is example project to present the bug in `@react-navigation/stack` in older Safari versions.

## Steps to reproduce

Clone this repo or follow steps 1-3.

1. Create new project with 

`npx create-expo-app@latest --template blank-typescript`


2. `cd` into created project and install dependencies:

```
npx expo install react-native-web react-dom @react-navigation/native @react-navigation/stack @react-navigation/native-stack react-native-screens react-native-safe-area-context @expo/metro-runtime
```


3. Replace `App.tsx` with:
```tsx
import { Text, View } from 'react-native';

import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';


function HomeScreen() {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Home Screen test</Text>
    </View>
  );
}

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={HomeScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

4. Run `npx expo export -p web`
5. Run server for hosting created directory, eg. `npx serve -p 4000 dist`]
6. Open Safari version 14.1.2 (16611.3.10.1.16)
7. Go to `http://localhost:4000`
8. Page should be blank
9. Open Javascript Console
10. Observe the error:
> `ReferenceError: Can't find variable: f`
11. Refresh the page
12. Page is loaded correctly, no error visible in the console.
13. Close console.
14. Refresh the page.
15. Page is blank again.

