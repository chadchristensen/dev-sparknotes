# React Native

## Table of Contents
### 1. [Components and JSX](#1-components-and-jsx-1):
Understanding how to create and compose components using JSX is foundational. This includes functional components, class components, and props.

### 2. [State and Props Management](#2-state-and-props-management-1):
 Mastering how to manage state within components, how to pass data via props, and how to handle user input and events.

### 3. [Navigation](#3-navigation-1):
Learn how to implement navigation between screens using libraries like React Navigation, including stack, tab, and drawer navigators.

### 4. [Styling and Layout](#4-styling-and-layout-1):
Get comfortable with React Native’s styling system, which is based on Flexbox, and how to create responsive designs that work on multiple screen sizes.

### 5. [API Integration and Networking](#5-api-integration-and-networking-1):
Understand how to make network requests using fetch or Axios, handle asynchronous data with Promises, and interact with APIs.

### 6. [Native Modules and Platform-Specific Code](#6-native-modules-and-platform-specific-code-1):
Learn how to leverage platform-specific code (iOS and Android) and how to use native modules to access device features like the camera or GPS.

### 7. [Debugging and Performance Optimization](#7-debugging-and-performance-optimization-1):
Get familiar with debugging tools (like React Native Debugger and Flipper) and learn how to optimize performance, such as handling large lists with FlatList and managing memory usage.

### 8. [State Management Libraries (e.g., Redux or Context API)](#8-state-management-libraries):
While basic state management can be done with React's built-in useState and useEffect, learning Redux or Context API will help manage more complex state across your application.

## 1. Components and JSX
### Understanding Components and JSX
Components are the building blocks of a React Native application. Each component in React Native is a self-contained piece of UI, which can be reused and combined to build complex user interfaces. JSX (JavaScript XML) is a syntax extension for JavaScript that looks similar to HTML but is used to describe what the UI should look like in React Native.

### React Native-Specific Components
React Native provides a set of built-in components that are specifically designed for mobile applications. Here are some of the most commonly used React Native components:

* **View:** The most fundamental component in React Native, similar to a div in web development. It’s used to create layout containers for other components.

    ```jsx
    import { View } from 'react-native';

    const MyComponent = () => (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
        {/* Other components go here */}
    </View>
    );
    ```

* **Text:** Used to display text in your app. In React Native, all text must be wrapped in a Text component.

    ```jsx
    import { Text } from 'react-native';

    const MyText = () => <Text>Hello, React Native!</Text>;
    ```

* **Image:** Used to display images in your app. It supports various image formats and can load images from different sources (local or remote).

    ```jsx
    import { Image } from 'react-native';

    const MyImage = () => (
    <Image
        source={{ uri: 'https://example.com/my-image.png' }}
        style={{ width: 100, height: 100 }}
    />
    );
    ```

* **ScrollView:** A container that provides scrolling capabilities when the content inside it is too large to fit on the screen. It’s useful for creating vertically or horizontally scrollable content.

    ```jsx
    import { ScrollView, Text } from 'react-native';

    const MyScrollView = () => (
    <ScrollView>
        <Text>Content goes here...</Text>
    </ScrollView>
    );
    ```

* **FlatList:** An optimized component for rendering large lists of data efficiently. It’s highly customizable and supports features like infinite scrolling, pull-to-refresh, and item separators.

    ```jsx
    import { FlatList, Text } from 'react-native';

    const MyList = () => {
    const data = [{ key: 'Item 1' }, { key: 'Item 2' }, { key: 'Item 3' }];

    return (
        <FlatList
        data={data}
        renderItem={({ item }) => <Text>{item.key}</Text>}
        />
    );
    };
    ```

* **TouchableOpacity:** A wrapper for making views respond to touches. When pressed, the opacity of the wrapped view is decreased, giving feedback to the user. This is commonly used for buttons.

    ```jsx
    import { TouchableOpacity, Text } from 'react-native';

    const MyButton = () => (
    <TouchableOpacity onPress={() => alert('Button pressed!')}>
        <Text>Press Me</Text>
    </TouchableOpacity>
    );
    ```

* **TextInput:** A basic component for user input. It allows users to enter text, and you can handle the input using event handlers like onChangeText.

    ```jsx
    import { TextInput } from 'react-native';
    import { useState } from 'react';

    const MyTextInput = () => {
    const [text, setText] = useState('');

    return (
        <TextInput
        value={text}
        onChangeText={setText}
        placeholder="Type something..."
        />
    );
    };
    ```

* **Button:** A basic button component that displays a button with a label and triggers an action when pressed.

    ```jsx

    import { Button } from 'react-native';

    const MyButton = () => (
    <Button
        title="Press Me"
        onPress={() => alert('Button pressed!')}
    />
    );
    ```

* **Modal:** A component used to present content above an enclosing view, often used for dialogs, prompts, or popups.

    ```jsx
    import { Modal, View, Text, Button } from 'react-native';
    import { useState } from 'react';

    const MyModal = () => {
    const [modalVisible, setModalVisible] = useState(false);

    return (
        <View>
        <Button title="Show Modal" onPress={() => setModalVisible(true)} />
        <Modal visible={modalVisible} transparent={true}>
            <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <View style={{ backgroundColor: 'white', padding: 20 }}>
                <Text>Modal Content</Text>
                <Button title="Close" onPress={() => setModalVisible(false)} />
            </View>
            </View>
        </Modal>
        </View>
    );
    };
    ```

## 2. State and Props Management

## 3. Navigation

## 4. Styling and Layout

## 5. API Integration and Networking

## 6. Native Modules and Platform-Specific Code

## 7. Debugging and Performance Optimization

## 8. State Management Libraries
