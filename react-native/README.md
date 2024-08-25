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
State and props are crucial concepts in React Native (and React in general), as they determine how your app's UI behaves and responds to user interactions.

### Props in React Native
**Props** (short for "properties") are used to pass data from a parent component to a child component. They are read-only, meaning the child component cannot modify them; they are meant to configure the child component.

#### Key Points about Props:

* Props are passed down from a parent component to a child component.
* They are immutable within the child component.
* Props allow you to pass data and event handlers to child components.
* A child component can access props via this.props in class components or directly as a parameter in functional components.

**Example**
```jsx
import React from 'react';
import { View, Text } from 'react-native';

const Greeting = (props) => {
  return (
    <Text>Hello, {props.name}!</Text>
  );
};

const App = () => {
  return (
    <View>
      <Greeting name="John" />
      <Greeting name="Jane" />
    </View>
  );
};
```

In this example, the `Greeting` component receives the `name` prop from the parent component (`App`), allowing it to display different greetings based on the prop value.

### State in React Native
**State** is used to manage data that can change over time. Unlike props, state is mutable and can be updated based on user interactions, API responses, or other events within the component.

#### Key Points about State:
* State is managed within the component and can be changed using the `setState` function in class components or the `useState` hook in functional components.
* Changes in state trigger a re-render of the component, allowing the UI to update in response to state changes.
* State is useful for handling dynamic data, such as user input, fetched data, or the result of user actions.

Example using Functional Components with useState:
```jsx
import React, { useState } from 'react';
import { View, Text, Button } from 'react-native';

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <View>
      <Text>Count: {count}</Text>
      <Button title="Increase" onPress={() => setCount(count + 1)} />
      <Button title="Decrease" onPress={() => setCount(count - 1)} />
    </View>
  );
};

const App = () => {
  return (
    <View>
      <Counter />
    </View>
  );
};
```

In this example, the **`Counter`** component manages its own state (count). The state is initialized to 0 using the useState hook, and it's updated whenever the "Increase" or "Decrease" button is pressed, which triggers a re-render to display the updated count.

### Props vs. State in React Native
* **Props** are passed to components, whereas state is managed within components.
* **Props** are used to configure a component and should not change (immutable), while state is dynamic and can change over time (mutable).
* Components re-render when their **state** changes, allowing the UI to reflect the latest data.

### Handling User Input with State
A common use case for state in React Native is managing user input, such as text entered into a TextInput field. Here's how you can handle and manage user input using state:

```jsx
import React, { useState } from 'react';
import { View, TextInput, Text } from 'react-native';

const InputComponent = () => {
  const [inputValue, setInputValue] = useState('');

  return (
    <View>
      <TextInput
        value={inputValue}
        onChangeText={text => setInputValue(text)}
        placeholder="Type something..."
        style={{ height: 40, borderColor: 'gray', borderWidth: 1, marginBottom: 20 }}
      />
      <Text>You typed: {inputValue}</Text>
    </View>
  );
};

const App = () => {
  return (
    <View>
      <InputComponent />
    </View>
  );
};
```

In this example, the InputComponent manages the state of the TextInput value. As the user types, the inputValue state is updated via the onChangeText handler, and the component re-renders to display the current input.

### Using State and Props Together
Often, you'll use state in combination with props. For example, you might fetch data in a parent component, store it in the state, and then pass that data down to child components as props.

```jsx
import React, { useState, useEffect } from 'react';
import { View, Text } from 'react-native';

const DataDisplay = ({ data }) => {
  return <Text>{data}</Text>;
};

const App = () => {
  const [data, setData] = useState('Loading...');

  useEffect(() => {
    // Simulate fetching data
    setTimeout(() => {
      setData('Fetched Data');
    }, 2000);
  }, []);

  return (
    <View>
      <DataDisplay data={data} />
    </View>
  );
};
```

In this example, the **`App`** component fetches data and stores it in its state. The DataDisplay component receives the fetched data as a prop and displays it. Initially, the state is "Loading...", and after 2 seconds, it updates to "Fetched Data," demonstrating how state and props work together to manage and display dynamic data.

Mastering state and props in React Native will enable you to build interactive and dynamic mobile applications, allowing components to communicate effectively and react to user interactions.

## 3. Navigation

## 4. Styling and Layout

## 5. API Integration and Networking

## 6. Native Modules and Platform-Specific Code

## 7. Debugging and Performance Optimization

## 8. State Management Libraries
