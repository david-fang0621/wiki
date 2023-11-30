1. Basic Concept

- SafeAreaView
  At the below of Status Bar (Top Bar) of the devices
- Expo CLI vs React native CLI
  React Native recommends using the React Native CLI if you are already familiar with Mobile App Development. However, if you are new to mobile app development and want to get the project quickly set up, Expo CLI is recommended.
  ![[Pasted image 20220616001119.png]]
- Scrollview vs Flatlist
  Scrollview renders all the content, so it's non-profit for long content, but flatlist is rendered whenever the content is visible
- android_ripple
- Flatlist - numColumns
- Expo icon: @expo/vector-icons Material Icons, Ion Icons
- Expo font

```
import {useFonts} from 'expo-font';

const [fontsLoaded] = useFonts({
	'open-sans': require('./assets/fonts/OpenSans-Regular.ttf')
})

if (!fontsLoaded) {
	return <AppLoading />;
}
```

- Expo app loading
- Image source

```
<Image source={require('../assets/images/car.png')} />
<Image source={ uri: imageURL } />
```

- Nested Text
  <Text><Text></Text></Text>
- useNavigation hook

```
import {useNavigation, useRoute} from '@react-navigation/native';
const navigation = useNavigation();

// pass params
navigation.navigate('Home', { categoryId: id});

// recive params using navigation
const { categoryId } = route.params;

// set options
navigation.setOptions({ title: "Meal Overview" });
```

1. Adaptive & Responsive UIs

- Dimensions

```
const deviceWidth = Dimensions.get('window').width;
```

- Screen Orientation
  useWindowDimensions hook from react-native
- KeyboardAvoidingView

```
import {KeyboardAvoidingView} from 'react-native';

<ScrollView>
	<KeyboardAvoidingView behavior="position" style={{flex: 1}}>
	</KeyboardAvoidingView>
</ScrollView>
```

- Platform

```
import {Platform} from 'react-native';

Platform.OS === 'android'
borderWidth: Platform.select({ios: 0, android: 2})
```

- change file name as 'Title.android.js, Title.ios.js'

### How Exactly Does Expo Work?

Expo Go App (shared native runtime) <- Loaded into Expo client app ("Expo Go") <-

- App development
- Your code
- You don't build real app executables during development. Instead, your source code is injected into the Expo Go client app (and executed there)

### Expo Alternatives

1. Expo "Managed Workflow"

- Easy to set up & work with
- Quick & frictionless development
- No or very little configuration required
- You can build (cross-platform) standalone apps

1. Expo "Bare Workflow"

- Easy to set up & work with
- Convenient development
- Some configuration required
- You can build (cross-platform) standalone apps

1. React Native CLI

- More complex setup
- Convenient development
- Can require more configuration effort
- Standalone apps are built locally

### Configuring Android APps

As shown earlier in the course (when adding native modules to non-Expo apps), you can manage certain aspects of your Android app with the AndroidManifest.xml file.

There, you can configure three important things:

- The **App name** as it appears on the home screen: https://stackoverflow.com/questions/5443304/how-to-change-an-android-apps-name
- The **bundle identifier & package name** of the app (also requires tweaking in other files): https://developer.android.com/studio/build/application-id
- The **permissions** of the app: https://developer.android.com/guide/topics/manifest/manifest-intro#perms

You should also set an **app version** and change it with every app update. This is done in the build.gradle file, see: https://developer.android.com/studio/publish/versioning

### Local Notifications -Permissions

When using Expo Go, you shouldn't need to ask for any permissions to send or show local notifications (or notifications in general).

This will change as you build your app for production though. Even when using Expo's managed workflow, you will then leave the Expo Go app (as a standalone app will be built by EAS - see section 14).

To ensure that notifications work correctly, you should therefore ask for permission. For Android, no changes are required. For iOS, you can use the `getPermissionsAsync()` method ([documentation](https://docs.expo.dev/versions/latest/sdk/notifications/#getpermissionsasync-promisenotificationpermissionsstatus)) provided by `expo-notifications` to get the current permission status. You can use `requestPermissionsAsync()` ([documentation link](https://docs.expo.dev/versions/latest/sdk/notifications/#requestpermissionsasyncrequest-notificationpermissionsrequest-promisenotificationpermissionsstatus)) to request permissions.

A full code example can be found [here](https://docs.expo.dev/push-notifications/push-notifications-setup/) but **I will also walk you through the entire permission setup later in this section as well.**
