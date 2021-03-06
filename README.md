# react-native-mpchart

A React Native chart library

This module is a bridge between [React Native](https://facebook.github.io/react-native/) and [MPAndroidChart](https://github.com/PhilJay/MPAndroidChart). Eventually, iOS will be supported via the iOS port of MPAndroidChart, [ios-charts](https://github.com/danielgindi/ios-charts).

All charts and properties come from MPAndroidChart.

## Installation

### Android

#### Install the node package

`npm install --save https://github.com/mikemonteith/react-native-mpchart`

#### Import the java library from `node_modules/react-native-mpchart/android`

*android/settings.gradle*
```
include ':react-native-mpchart', ':app'

project(':react-native-mpchart').projectDir = new File(settingsDir, '../node_modules/react-native-mpchart/android')
```

*android/app/build.gradle*
```
apply plugin: 'com.android.application'

android {
  ...
}

dependencies {
  compile fileTree(include: ['*.jar'], dir: 'libs')
  compile 'com.android.support:appcompat-v7:23.0.0'
  compile 'com.facebook.react:react-native:0.17.+'
  compile project(':react-native-mpchart')
}

```

Add the package to your ReactInstanceManager

*MainActivity.java*
```java

//import chart package (usually, your IDE will do this for you)
import com.mikemonteith.reactnativempchart.MPChartPackage;

// ...
mReactInstanceManager = ReactInstanceManager.builder()
                .setApplication(getApplication())
                .setBundleAssetName("index.android.bundle")
                .setJSMainModuleName("index.android")
                .addPackage(new MPChartPackage()) // <-- add this line
                .setUseDeveloperSupport(BuildConfig.DEBUG)
                .setInitialLifecycleState(LifecycleState.RESUMED)
                .build();
// ...
```

## Basic Usage

```js
var React = require('react-native');
var Charts = require('react-native-mpchart');

var ExampleComponent = React.createClass({
  render: function(){
    return (
      <Charts.BarChart
        style={{flex: 1}}
        data={{
          dataSets: [{
            values: [1, 2, 3, 4, 5],
          }],
          xValues: ["one", "two", "three", "four", "five"],
        }}
      />
    );
  },
});
```

## Charts

* PieChart
* BarChart
* LineChart

## Props
(inherits from [React.View](https://facebook.github.io/react-native/docs/view.html#props))

| Prop | Description | Type | Charts |
|------|-------------|------|--------|
| data | see [data properties](#data-properties) | object | All
| touchEnabled | handle touch gestures on the chart | boolean | All
| xAxis | see [xaxis properties](#x-axis-properties) | object | Bar, Line
| leftAxis | see [yaxis properties](#y-axis-properties) | object | Bar, Line
| rightAxis | see [yaxis properties](#y-axis-properties) | object | Bar, Line
| gridBackgroundColor | color of the grid background | string | Bar, Line

#### data properties

| Property | Description | Type | Charts |
|----------|-------------|------|--------|
| dataSets | see [dataSet properties](#dataSet-properties) | array of DataSet objects | All |
| xValues | strings specifying x axis labels | array of strings | All |

#### dataSet properties

| Property | Description | Type | Charts |
|----------|-------------|------|--------|
| values | values to plot on the graph | array of numbers | All
| colors | colors to draw the chart data | array of strings | All
| drawValues | draw value text | boolean | All
| drawCircles | draw circles on data points | boolean | Line
| drawCubic | draw a smooth line-of-best-fit | boolean | Line
| lineWidth | width of the line-of-best-fit | boolean | Line

#### axis properties

| Property | Description | Type | Charts |
|----------|-------------|------|--------|
| enabled | draw the axis | boolean | Bar, Line |
| drawAxisLine | draw the main axis line | boolean | Bar, Line
| drawGridLines | draw grid lines that are parallel to this axis | boolean | Bar, Line

#### x axis properties
(inherits from [axis properties](#axis-properties))

| Property | Description | Type | Charts |
|----------|-------------|------|--------|
| position | where to draw the axis | string `'bottom'`, `'top'` or `'bothSided'` | Bar, Line

#### y axis properties
(inherits from [axis properties](#axis-properties))

| Property | Description | Type | Charts |
|----------|-------------|------|--------|
| minValue | minimum value | number | Bar, Line
| maxValue | maximum value | number | Bar, Line
| inverted | if true, draw the data upside-down | boolean | Bar, Line


## TODO

* Support all MPAndroidChart charts
* Support all MPAndroidChart properties
* Support iOS
* Release as npm package
