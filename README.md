# Wdatepicker

[![Build Status](https://travis-ci.org/wujiabk/datepicker.svg?branch=master)](https://travis-ci.org/wujiabk/datepicker)
[![npm](https://img.shields.io/npm/v/@wujiaxian/datepicker)](https://www.npmjs.com/package/@wujiaxian/datepicker)
[![npm bundle size](https://img.shields.io/bundlephobia/min/@wujiaxian/datepicker)](https://www.npmjs.com/package/@wujiaxian/datepicker)
[![npm](https://img.shields.io/npm/dm/@wujiaxian/datepicker)](https://www.npmjs.com/package/@wujiaxian/datepicker)
[![GitHub issues](https://img.shields.io/github/issues/wujiabk/datepicker)](https://github.com/wujiabk/datepicker/issues)
[![npm](https://img.shields.io/npm/l/@wujiaxian/datepicker)](https://www.npmjs.com/package/@wujiaxian/datepicker)

A C-End Date Selector Component Based on Vue Development.

- [Demo](#demo)
- [Install](#install)
- [Usage](#usage)
- [Date Formatting](#date-formatting)
- [Props](#available-props)
- [Events](#events)
- [Slots](#Slots)
- [Disabled dates](#disabled-dates)
- [Internationalization](#Internationalization)

## Demo

To view a demo online:
https://codesandbox.io/embed/staging-darkness-k7ymp

To view demo examples locally clone the repo and run `npm install && npm run dev`

## Install

``` bash
npm install @wujiaxian/datepicker --save
```


``` javascript
import Vue from 'vue'
import Wdatepicker from '@wujiaxian/datepicker'
import "@wujiaxian/datepicker/dist/Wdatepicker.css"

Vue.use(Wdatepicker)
```

Or use directly from a CDN
``` html
<head>
  <link href="https://unpkg.com/@wujiaxian/datepicker/dist/Wdatepicker.css"/>
</head>
<div id="app">
  <w-datepicker></w-datepicker>
</div>
<script src="https://unpkg.com/vue"></script>
<script src="https://unpkg.com/@wujiaxian/datepicker"></script>
<script>
  const app = new Vue({
    el: '#app'
  })
</script>
```

## Usage

``` html
<w-datepicker></w-datepicker>
```
*value* prop if passed should be a Date object or String Date Formatting or Number time stamp

``` html
<script>
export default {
  data () {
    return {
      date: new Date('2019-09-30')
    }
  }
}
</script>
<w-datepicker :value="date"></w-datepicker>
```

Using `v-model`
``` html
<w-datepicker v-model="date"></w-datepicker>
```

Using 'v-model and defaultValue'
``` html
<script>
export default {
  data () {
    return {
      date: ''
    }
  }
}
</script>
<w-datepicker v-model="date" defaultValue="2019-09-30"></w-datepicker>
```

Emits events
``` html
<script>
export default {
  data () {
    return {
      date: ''
    }
  },
  methods: {
    change (value) {

    },
    focus (componentInstance) {

    },
    blur (componentInstance) {

    },
    // Click is not the date of that month, switch to that month or select the date of that month or do nothing. Operations are prohibited at times other than maximum and minimum.
    disabledDate ({ year, month, date, disabledDate, thisMonth }) {

    }
  }
}
</script>
<w-datepicker v-model="date" @changge="change" @focus="focus" @blur="blur" @disabledDate="disabledDate"></w-datepicker>
```


## Date Formatting

String Formatting

| Token | Desc                   | Example     |
|-------|------------------------|-------------|
| YYYY  | year                   | 2019        |
| MM    | month                  | 01          |
| DD    | date                   | 30          |
| hh    | hour                   | 12          |
| mm    | minute                 | 30          |
| ss    | second                 | 30          |


Number time stamp

1569572985 // second

1569572985000 // Millisecond

Date Object

new Date('2019/09/30')

## Available props

| Prop                          | Type                    | Default                 | Description                              |
|-------------------------------|-------------------------|-------------------------|------------------------------------------|
| value / v-model               | Date\|String\|Number    |                         | Date value of the datepicker             |
| defaultValue                  | Date\|String\|Number    |                         | Date selector default date value         |
| editable                      | Boolean                 | false                   | Whether the input box can be entered     |
| formatDate                    | String                  | YYYY-MM-DD              | The format displayed in the input box    |
| minDate                       | Date\|String\|Number    | Ten years ago           | Minimum time                             |
| maxDate                       | Date\|String\|Number    | Ten Years From Now      | Maximum time                             |
| clickDisabledDate             | String                  |                         | Click on the non-current month date, select the month date when the value is empty, switch to that month when the value is switch, and the other values do not operate.|
| placeholder                   | String                  | Selection date          | Input box prompt information             |
| selectState                   | String                  | circle                  | Time Selected State, Value: Square or Round or Empty|
| clearBtn                      | Boolean                 | true                    | Whether the Clear button is displayed or not|
| disabled                      | Boolean                 | false                   | Prohibition of use                       |
| disabledDate                  | Array\|Function         | []                      | Disabled date                            |
| closeIconClass                | String                  |                         | Close the button class, you can set icon class to replace the current one| String                  |                         | Time icon class, you can set icon class to replace the current

## Events

| Event                         | Output                    | Description                              |
|-------------------------------|---------------------------|------------------------------------------|
| change                        | String                    | Triggered after the time has been changed to receive the changed value|
| focus                         | Object                    | Input box gets focus trigger and receives component instance  |
| blur                          | Object                    | Input box lost focus trigger, receive component instance |
| disabledDate                  | Object                    | To receive the current date information, click on a callback from a non-current month date or a banned date |

## Slots

| Name                          | params                    | Description                              |
|-------------------------------|---------------------------|------------------------------------------|
| header                        | component instance, {self}| Date Selection Box Header Insert Content |        
| footer                        | component instance, {self}| Insert content at the bottom of the date selection box  |
| date-icon                     |                           | Custom Date Icon                         |
| close-icon                    |                           | Custom Close Icon                        |


#### Use of slots
``` html
<script>
export default {
  data () {
    return {
      date: ''
    }
  },
  methods: {
    headClickHandler (componentInstance) {

    },
    switchingDate (componentInstance, type) {
      let now = new Date()
      let cnow = new Date(this.date)
      switch (type) {
        case 'front':
          cnow.setDate(cnow.getDate() - 10)
          break
        case 'after':
          cnow.setDate(cnow.getDate() + 10)
          break
      }
      const t = type === 'now' ? now : cnow
      componentInstance.selectDate(t)
    }
  }
}
</script>

<w-datepicker v-model="date">
  <template v-slot:header="{self}">
    <div @click="headClickHandler(self)">This is a head content.</div>
  </template>

  <template v-slot:footer="{self}">
    <button @click="switchingDate(self, 'front')">The first 10 days</button>
    <button @click="switchingDate(self, 'now')">Today<button>
    <button @click="switchingDate(self, 'after')">The next 10 days</button>
  </template>
</w-datepicker>
```

## Disabled Dates

Dates can be disabled in a number of ways.

Array mode
``` html
<script>
export default {
  data () {
    return {
      disableDate: ['2019-09-18', '2019-09-08']
    }
  }
}
</script>

<w-datepicker v-model="date" :disabledDate="disableDate"></w-datepicker>
```

Function mode
``` html
<script>
export default {
  data () {
    return {
      date: ''
    }
  },
  methods: {
    disableDate (currentDate, monthDate, nowDate) {
      let date = new Date('2019/09/10')
      return date.getFullYear() === monthDate.getFullYear() && date.getMonth() === monthDate.getMonth() && date.getDate() === monthDate.getDate()
    }
  }
}
</script>

<w-datepicker :disabledDate="disableDate"></w-datepicker>
```


## Internationalization

The default use of Chinese in components is required. If you want to use other languages, you need to have multiple language settings. Take English as an example, in main.js:

``` html
<script>
  // Complete introduction
  import Vue from 'vue'
  import Wdatepicker from '@wujiaxian/datepicker'
  import "@wujiaxian/datepicker/dist/Wdatepicker.css"
  import en from '@wujiaxian/datepicker/dist/lib/locale/lang/en'

  Vue.use(Wdatepicker, { 
    locale: en 
  })

  // or

  Vue.use(Wdatepicker)
  Wdatepicker.locale(en)

  // or

  import locale from '@wujiaxian/datepicker/dist/lib/locale/index'

  locale.use(en)
  Vue.use(Wdatepicker)
</script>
``` 

#### compatible vue-i18n@6.x

Vue-i18n of 6.x is not supported by default. You need to process it manually.

``` html
<script>
  import Vue from 'vue'
  import Wdatepicker from '@wujiaxian/datepicker'
  import "@wujiaxian/datepicker/dist/Wdatepicker.css"
  import en from '@wujiaxian/datepicker/dist/lib/locale/lang/en'

  Vue.use(VueI18n)

  const i18n = new VueI18n({
    locale: 'en',
    message: {
      en: {
        ...en
      },
      cn: {
        //...cn
      }
    }
  })

  Vue.use(Wdatepicker, {
    i18n: (key, value) => i18n.t(key, value)
  })

  new Vue({ i18n }).$mount('#app')
</script>
``` 

or

``` html
<script>
  import Vue from 'vue'
  import Wdatepicker from '@wujiaxian/datepicker'
  import "@wujiaxian/datepicker/dist/Wdatepicker.css"
  import en from '@wujiaxian/datepicker/dist/lib/locale/lang/en'
  import locale from '@wujiaxian/datepicker/dist/lib/locale/index'

  Vue.use(VueI18n)
  Vue.use(Wdatepicker)

  const i18n = new VueI18n({
    locale: 'en',
    message: {
      en: {
        ...en
      },
      cn: {
        //...cn
      }
    }
  })

  locale.i18n((key, value) => i18n.t(key, value))
</script>
``` 

#### Loading Language Files by CDN

```html
  <script src="https://unpkg.com/vue"></script>
  <script src="https://unpkg.com/@wujiaxian/datepicker"></script>
  <script src="https://unpkg.com/@wujiaxian/datepicker/dist/lib/locale/lang/en.js"></script>

  <script>
    Vue.use(Wdatepicker)
    Wdatepicker.locale(W.lang.en)

    // or

    Vue.use(Wdatepicker, {
      locale: W.lang.en
    })
  </script>
```

Matching vue-i18n usage

```html
  <script src="https://unpkg.com/vue"></script>
  <script src="https://unpkg.com/vue-i18n/dist/vue-i18n.js"></script>
  <script src="https://unpkg.com/@wujiaxian/datepicker"></script>
  <script src="https://unpkg.com/@wujiaxian/datepicker/dist/lib/locale/lang/en.js"></script>

  <script>
    Vue.use(VueI18n)
    Vue.use(Wdatepicker)

    const messages = {
      ko: {
        ...W.lang.ko
      }
    }

    const i18n = new VueI18n({
      locale: 'ko',
      messages,
    })
    
    Wdatepicker.i18n((key, value) => i18n.t(key, value))
  </script>
```

#### At present, the following languages are built-in:

  - 简体中文（zh_CN）
  - 繁体中文（zh_TW）
  - English（en）
  - Japanese（ja）
  - Korean（ko）

#### If you need to add a language, please submit it it to me in the following file format.
[Languges](https://unpkg.com/@wujiaxian/datepicker/dist/lib/locale/lang/)

# License
[MIT](https://opensource.org/licenses/MIT)

Copyright (c) 2019-present, Jia Wu
