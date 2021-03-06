# csv-converter

A ruby script to convert [version 0.9](https://cricsheet.org/format/) [Cricsheet YAML data files](https://cricsheet.org/downloads/) into CSV.

The CSV generated is considered an **experimental** Cricsheet format. Originally CSV data was provided for only T20 and IPL matches, however that has now expanded to include all matches. The CSV version was originally created in response to a request for a simple version of the data in CSV format (rather than YAML). The data it generates is not as complete as the YAML data and, currently, does not fully support all fields. A list of [known limitations](#known-limitations) can be found below.

The data generated is similar to, but **not exactly the same as**, that provided on the [Cricsheet downloads](https://cricsheet.org/downloads/) page. The data generated by the `convert.rb` script does not include values for `season`, `match_number`, `series`, `reserve_umpire`, `tv_umpire`, or `match_referee`, unlike that provided on the website. A future version of this converter will include these fields.

## Installation

You can manage the dependencies using [Bundler](http://bundler.io/). Once you have it installed you can install the dependencies using:

```bash
$ bundle install
```

## Usage

`convert.rb` is a ruby script. It takes the path to a single match file (in version 0.9 YAML format), and outputs the generated CSV for the match.

### Examples

Convert a single YAML file, and print the resulting CSV to the command line.

```bash
$ ./convert.rb data.yaml
```

Convert a single YAML file, and write the resulting CSV to a file named `data.csv`.

```bash
$ ./convert.rb data.yaml > data.csv
```

## The format of the data

Each file has a 'version', multiple 'info' lines, and multiple 'ball' lines.
The 'version' is 1.2.0 right now, and will change as I make changes (in line 
with the [Semantic Versioning guidlines](http://semver.org/)). The 'info'
entries should be fairly self-explanatory but feel free to ask on
Twitter (@cricsheet) if you're unsure. If you look carefully you may see some
slight hints as to some data we'll be including in the full data files in
the future.

Each 'ball' line has the following fields:

  * The word 'ball' to identify it as such
  * Innings number, starting from 1
  * Over and ball
  * Batting team name
  * Batsman
  * Non-striker
  * Bowler
  * Runs-off-bat
  * Extras
  * Kind of wicket, if any. If more than one wicket fell on a delivery
    then the dismissal methods are separated by `, `.
  * Dismissed player, if there was a wicket. If more than one wicket
    fell on a delivery then the dismissed players are separated by `, `.

## Known limitations

There are a number of known limitations with the current CSV format. Discussion/feedback on how best to address these is welcome.

### Lack of detail for extras

At the moment each delivery merely shows how many extras were scored, and doesn't break that information down into the type of extras that were conceded. This is due to the original request for CSV data specially asking just for the total extras conceded per delivery.
