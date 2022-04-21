---
layout: default
title: Reproducibility Office Hours
permalink: /pages/office-hours
---

# Office Hours Information

We will be holding office hours to assist you and answer any questions you may have related to creating a Docker image of your code and submitting to our verification service for the [Reproducible Results Badge](/badges).

The table below has the times and calendar invites for the office hours.
The UTC times are the official times (please double check that the local time is correct).

The office hours will be held with Google Meet.
If these times do not work for you or you are unable to access Google Meet, please get in contact with us [via email](mailto:naacl-2022-reproducibility-track@googlegroups.com) or [Slack](https://join.slack.com/t/cs-b5i1449/shared_invite/zt-16nrrhflc-gPPQwvU7OQCEoO8YG393Ng).

<table>
  <tr>
    <th>Time (UTC)</th>
    <th>Time (Your Timezone)</th>
    <th>Calendar Event</th>
  </tr>
  <tr>
    <td id="0_utc"></td>
    <td id="0_local"></td>
    <td id="0_event"></td>
  </tr>
  <tr>
    <td id="1_utc"></td>
    <td id="1_local"></td>
    <td id="1_event"></td>
  </tr>
  <tr>
    <td id="2_utc"></td>
    <td id="2_local"></td>
    <td id="2_event"></td>
  </tr>
  <tr>
    <td id="3_utc"></td>
    <td id="3_local"></td>
    <td id="3_event"></td>
  </tr>
  <tr>
    <td id="4_utc"></td>
    <td id="4_local"></td>
    <td id="4_event"></td>
  </tr>
  <tr>
    <td id="5_utc"></td>
    <td id="5_local"></td>
    <td id="5_event"></td>
  </tr>
  <tr>
    <td id="6_utc"></td>
    <td id="6_local"></td>
    <td id="6_event"></td>
  </tr>
  <tr>
    <td id="7_utc"></td>
    <td id="7_local"></td>
    <td id="7_event"></td>
  </tr>
</table>

<script>
days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
months = ["April", "May"];

function getUTCDateString(date) {
    var day = days[date.getUTCDay()] + ", " + months[date.getUTCMonth() - 3] + " " + date.getUTCDate();
    var start = date.getUTCHours() + ":" + String(date.getUTCMinutes()).padStart(2, "0");
    var end = (date.getUTCHours() + 1) + ":" + String(date.getUTCMinutes()).padStart(2, "0");
    return day + ", " + start + "-" + end;
}

function getLocalDateString(date) {
    var day = days[date.getDay()] + ", " + months[date.getMonth() - 3] + " " + date.getDate();
    var start = date.getHours() + ":" + String(date.getMinutes()).padStart(2, "0");
    var end = (date.getHours() + 1) + ":" + String(date.getMinutes()).padStart(2, "0");
    return day + ", " + start + "-" + end;
}

dates = [
    new Date('2022-04-25T10:00:00.000Z'),
    new Date('2022-04-26T21:00:00.000Z'),
    new Date('2022-04-27T08:00:00.000Z'),
    new Date('2022-04-28T10:30:00.000Z'),
    new Date('2022-05-01T09:00:00.000Z'),
    new Date('2022-05-01T19:00:00.000Z'),
    new Date('2022-05-03T12:00:00.000Z'),
    new Date('2022-05-03T17:30:00.000Z'),
];

events = [
    "https://calendar.google.com/event?action=TEMPLATE&tmeid=N2Jjc2RjMWE2djNtcGo0ZW9xaXRhaWp0azQgZGRldXRzY2hAc2Vhcy51cGVubi5lZHU&tmsrc=ddeutsch%40seas.upenn.edu",
    "https://calendar.google.com/event?action=TEMPLATE&tmeid=MG9uN2g4a2I2ZmNmdHNwcDV2NjQ5dHM1cG4gZGRldXRzY2hAc2Vhcy51cGVubi5lZHU&tmsrc=ddeutsch%40seas.upenn.edu",
    "https://calendar.google.com/event?action=TEMPLATE&tmeid=NWZqNDkwaXBrZTVpbW81NnVzY2dvcGxkMmggZGRldXRzY2hAc2Vhcy51cGVubi5lZHU&tmsrc=ddeutsch%40seas.upenn.edu",
    "https://calendar.google.com/event?action=TEMPLATE&tmeid=NHVndWI2bWI2ZTRtdnY5aGIxMDlmZWhvZDkgZGRldXRzY2hAc2Vhcy51cGVubi5lZHU&tmsrc=ddeutsch%40seas.upenn.edu",
    "https://calendar.google.com/event?action=TEMPLATE&tmeid=M3UxMHZrMDE3YTJ1MnR1azhlN3FoZjlwOHUgZGRldXRzY2hAc2Vhcy51cGVubi5lZHU&tmsrc=ddeutsch%40seas.upenn.edu",
    "https://calendar.google.com/event?action=TEMPLATE&tmeid=NjFya3N1M2c4c3E5NmY0bmZoZjIwcDkyMmEgZGRldXRzY2hAc2Vhcy51cGVubi5lZHU&tmsrc=ddeutsch%40seas.upenn.edu",
    "https://calendar.google.com/event?action=TEMPLATE&tmeid=NjVqZGZhdjVyMTE2Y2gxa3ZobWR0czR1bXEgZGRldXRzY2hAc2Vhcy51cGVubi5lZHU&tmsrc=ddeutsch%40seas.upenn.edu",
    "https://calendar.google.com/event?action=TEMPLATE&tmeid=MDV2NHZoc3M4dGlwOWJsczY1bHRpN2lydmcgZGRldXRzY2hAc2Vhcy51cGVubi5lZHU&tmsrc=ddeutsch%40seas.upenn.edu",
];

dates.forEach((date, index) => {
    document.getElementById(index + "_utc").innerHTML = getUTCDateString(date);
    document.getElementById(index + "_local").innerHTML = getLocalDateString(date);
    document.getElementById(index + "_event").innerHTML = "<a href=\"" + events[index] + "\">Link</a>";
});

</script>
