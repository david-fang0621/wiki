## ScrollView vs FlatList

The ScrollView works best to present a small number of things of a limited size. All the elements and views of a `ScrollView` are rendered, even if they are not currently shown on the screen. If you have a long list of items that cannot fit on the screen, you should use a `FlatList` instead.

## SectionList

sections, renderItem, renderSectionHeader, keyExtractor

## Platform

Platform.OS: ios, android

Platform.select: ios, android, native, default

Platform.Version : # android version

parseInt(Platform.Version, 10): # ios version

Platform-specific extensions: When your platform-specific code is more complex, you should consider splitting the code out into separate files. React Native will detect when a file has a `.ios.` or `.android.` extension and load the relevant platform file when required from other components.

## Fast Refresh

- Fast Refresh preserves React local state in function components (and Hooks) by default.
- Sometimes you might want to *force* the state to be reset, and a component to be remounted. For example, this can be handy if you're tweaking an animation that only happens on mount. To do this, you can add `// @refresh reset` anywhere in the file you're editing. This directive is local to the file, and instructs Fast Refresh to remount components defined in that file on every edit.
- `useState` and `useRef` preserve their previous values
- `useEffect`, `useMemo`, and `useCallback`—will *always* update during Fast Refresh.

## Testing

Unit Tests, Mocking, Integration Tests, Component Tests, End-to-End Tests

## Performance

- remove all `console.*` calls in the release (production) versions of your project.
  ```jsx
  npm i babel-plugin-transform-remove-console --save-dev

  # .babelrc
  {
    "env": {
      "production": {
        "plugins": ["transform-remove-console"]
      }
    }
  }
  ```
- If your `[FlatList](https://reactnative.dev/docs/flatlist)` is rendering slow, be sure that you've implemented `[getItemLayout](https://reactnative.dev/docs/flatlist#getitemlayout)` to optimize rendering speed by skipping measurement of the rendered items.
- Animated API vs LayoutAnimation
- Sometimes, if we do an action in the same frame that we are adjusting the opacity or highlight of a component that is responding to a touch, we won't see that effect until after the `onPress` function has returned.
  ```jsx
  handleOnPress() {
    requestAnimationFrame(() => {
      this.doExpensiveAction();
    });
  }
  ```
- Optimizing Flatlist configuration
  - **removeClippedSubviews - default: false**
  - **maxToRenderPerBatch - default: 10**
  - **updateCellsBatchingPeriod**
  - **initialNumToRender - default: 10**
  - **windowSize**
  # List Items
  - **Use basic components[](https://reactnative.dev/docs/optimizing-flatlist-configuration#use-basic-components)**
  - **Use light components[](https://reactnative.dev/docs/optimizing-flatlist-configuration#use-light-components)**
  - **Use shouldComponentUpdate[](https://reactnative.dev/docs/optimizing-flatlist-configuration#use-shouldcomponentupdate)**
  - **Use cached optimized images[](https://reactnative.dev/docs/optimizing-flatlist-configuration#use-cached-optimized-images)**
  - **Use getItemLayout[](https://reactnative.dev/docs/optimizing-flatlist-configuration#use-getitemlayout)**
  - **Use keyExtractor or key**
  - **Avoid anonymous function on renderItem**
    ```jsx
    const renderItem = useCallback(({item}) => (
       <View key={item.key}>
          <Text>{item.title}</Text>
       </View>
     ), []);

    return (
      // ...

      <FlatList data={items} renderItem={renderItem} />;
      // ...
    );
    ```

## Image

- If you need to scale the image dynamically (i.e. via flex), you may need to manually set `{width: undefined, height: undefined}` on the style attribute.
- border radius style properties might be ignored by iOS's image component:
- A common feature request from developers familiar with the web is `background-image`. To handle this use case, you can use the `<ImageBackground>` component
-
