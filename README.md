# Bonsai

Although Facebook develops the React Native framework, they delegated the role of developing a CLI tool to the community. As a result, several solutions emerged in the community. There are tools like [Expo](https://docs.expo.io/) that combine a framework and tooling around it, and [react-native-community/cli](https://github.com/react-native-community/cli) that is considered the official CLI.

As a user taking the first steps with React Native, **Expo** provides convenient workflows, packages, and services so that you don't have to leave the Expo ecosystem. However, that convenience comes with the cost of strong dependency on the Expo environment, which is oriented towards selling services: _projects are structured the Expo way and they have their [own solution](https://docs.expo.io/bare/installing-unimodules/) for setting up their modules_. At some point, users feel they need that convenience but without being tied to their ecosystem.

The official React Native CLI doesn't have such a strong dependency on an ecosystem. It provides useful commands, auto-linking of native code, and a build pipeline that can be used by Gradle and Xcode build to run [Metro](https://facebook.github.io/metro/) alongside the app. However, it doesn't solve two common inconveniences that developers are still facing these days: _upgrading RN is painful, and requiring Ruby & CocoaPods for linking the native iOS code adds an unnecessary indirection and make the user-experience error-prone._

Bonsai is an attempt to take a different approach:

- **Project generation** Xcode projects and `build.gradle` files are an implementation detail required to compile the app. Therefore, Bonsai could generate them when needed and ensure they have the right structure for a given RN version.
- **Built-in linking:** Bonsai could leverage the project generation phase on iOS to auto-link the native code of third-party dependencies pulled by NPM/Yarn. Like react-native-cli does, but without having to run `cd ios && pod install`, nor having to make sure that the Xcode project is properly configured.
- **Opinions:** Like [Rails](https://rubyonrails.org/) or [Redwood](https://redwoodjs.com/), Bonsai could make decisions on behalf of users to simplify the configuration, and bring them more focus.

Although it builds upon ideas from Expo and the react-native-cli, we are building this as a new tool to be able to prototype and validate the aforementioned ideas with ease. Those tools are mature and thus introducing such a radical change to their design would be a tedious process that would imply getting approval from the community and align all the maintainers of the tool. Moreover, it'd be challenging to safely migrate users to the new approach without breaking anything on their end.

We believe that Bonsai can be another valid approach to manage React Native projects and that users should be free to pick the one that aligns best with their needs.
