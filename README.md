
UK Local Authority Coronavirus Rates Checker
============================================

This is a small script designed to act as a custom Waybar module which
scrapes the UK Government's coronavirus data API to find the infection
rates in your local area.

## Usage

### Calling from the command line

```
covid-checker [Area Type] [Area Code]
```

The Area Type most be one of:
* utla (the highest level possible - eg Devon's)
* ltla (the medium size of region - eg North Devon)
* msoa (the smallest local area - eg Barnstaple South)

The Area Code should be the unique identifying code for the Local
Authority. Some examples:
* Devon: E10000008
* North Devon: E07000043
* Barnstaple South: E02004184
* Bristol: E06000023

Codes always start with a "E" for areas of England, "W" for areas within
Wales, "S" for Scotland, and "N" for Nothern Ireland.

You can use [FindThatPostCode][1] to help locate the correct code - you
must always use the one marked "local authority".

### Within Your WayBar config

```
{
    "modules-left": ["custom/covid"],

    "custom/covid": {
        # City of Bristol - see above for details of this line
        "exec": "covid-checker ltla E06000023",

        # Important as covid-checker always returns a Waybar's JSON format
        "return-type": "json",

        # {} will work on its own, but you may also want to add an icon or label
        "format": "{icon} {}",

        # If you want to show icons for up and down
        "format-icons": ["", ""]
    }
}
```

### Styling

The script returns unformatted text, so there's not a huge amount of
styling options, but if you named it `custom/covid` as shown above, you
can of course style the box with `#custom-covid`. If the rate is going
down, the classname for it will be set to `DOWN`, and it will be set to
`UP` if the rates are rising. A basic example of styling this:

```
#custom-covid.DOWN {
    color: green;
}

#custom-covid.UP {
    color: red;
}
```


[1]: https://findthatpostcode.uk/
