---
layout: post
title: Chartkick Charts with Percentage Style Stacked Charts
tags:
- percent
- percentage
- charts
- stacked
- gem
---

The Chartkick gem makes adding good looking charts to your Rails site really easy. It allows you to render Google Charts or HighCharts with ease.

One small thing that it didn't do was percentage (`percent`) or `relative` charts. These were already supported by Google Charts and HighCharts, so it was relatively easy to add this functionality to Chartkick.

I forked the project and added this functionality (as you can [see here](https://github.com/avjaarsveld/chartkick)), and [created a pull request](https://github.com/ankane/chartkick/pull/199) to get this added to the original gem.

## To Use Percentage Charts with Chartkick

1. While the pull request is pending, you'll need to change `gem 'chartkick'` to `gem 'chartkick', :git => 'git://github.com/avjaarsveld/chartkick.git'` in your Gemfile and run `bundle install`.

2. To keep your current Chartkick charts working and looking like they normally do, do nothing. `stacked: true` still works.

3. To make a Chartkick chart a stacked percent chart, add `stacked: "percent"` as an option, as shown in the example below.

### Example (from a haml view file):

```
= column_chart [{name: "Fail", data: @failing_assessment_count_by_month}, {name: "Pass", data: @passing_assessment_count_by_month}, {name: "Merit", data: @excelling_assessment_count_by_month}], stacked: "percent", colors: ["orange", "green", "gold"], library: {hAxis: {title: "Month Since Joining"}}
```

The above example will work if<br>
`@failing_assessment_count_by_month = [[0.0, 360], [1.0, 255], [2.0, 166]]` and<br>
`@passing_assessment_count_by_month = [[0.0, 870], [1.0, 905], [2.0, 766]]` and<br>
`@excelling_assessment_count_by_month = [[0.0, 450], [1.0, 1032], [2.0, 1209]]`<br>
(for example), which you'd set in the controller.

The result would look like this:
![Example Stacked Percent Chart](/images/example_stacked_percent_chartkick_chart.png)


