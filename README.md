# EM-Datepicker

## Demo
See a demo online: https://codesandbox.io/s/github/wishe/em-datepicker

To view a demo example locally clone the repo and run ```yarn install``` && ```yarn serve```

## Install
```
yarn add em-datepicker
```

```
import EmDatepicker from 'em-datepicker';

export default {
  // ...
  components: {
    EmDatepicker
  }
  // ...
}
```

Or from CDN

```
<script src="https://unpkg.com/em-datepicker@latest/dist/emDatepicker.umd.min.js"></script>
```

### Props

#### value

```
value: {
        from: undefined,
        to: undefined,
      },
```

#### language

```
language: 'localeString' eg. nbNO
```

#### disabled

```
disabled: {
    to: new Date(2016, 0, 5), // Disable all dates up to specific date
    from: new Date(2016, 0, 26), // Disable all dates after specific date
    days: [6, 0], // Disable Saturday's and Sunday's
    daysOfMonth: [29, 30, 31], // Disable 29th, 30th and 31st of each month
    dates: [ // Disable an array of dates
      new Date(2016, 9, 16),
      new Date(2016, 9, 17),
      new Date(2016, 9, 18)
    ],
    ranges: [{ // Disable dates in given ranges (exclusive).
      from: new Date(2016, 11, 25),
      to: new Date(2016, 11, 30)
    }, {
      from: new Date(2017, 1, 12),
      to: new Date(2017, 2, 25)
    }],
    // a custom function that returns true if the date is disabled
    // this can be used for wiring you own logic to disable a date if none
    // of the above conditions serve your purpose
    // this function should accept a date and return true if is disabled
    customPredictor: function(date) {
      // disables the date if it is a multiple of 5
      if(date.getDate() % 5 == 0){
        return true
      }
    }
  }
```

#### inputClass

```
inputClass: 'class' eg. form-control
```

#### wrapperClass

```
wrapperClass: 'class' eg. form-group
```

## Languages

Currently supported languages Norwegian (nbNO) and English (en) 