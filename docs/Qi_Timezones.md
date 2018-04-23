Qi Timezones
============


``GetTimeZonesAsync()``
-------------------

Returns a list of timezones.

**Syntax**

.. highlight:: none

::

    Task<IList<QiTimeZone>> GetTimeZonesAsync();

**Http**

::

    GET /qi/TimeZones


**Parameters**

``string Id``
  The unique Id of the time zone.
``string Name``
  The display name of the time zone.


Security
  Allowed by administrator and user accounts.

**Returns** 
  Returns a list of time zones.
  
  Sample return of JSON:

.. code:: javascript

  [
    {
      "Id": "Dateline Standard Time",
      "Name": "(UTC-12:00) International Date Line West"
    },
    {
      "Id": "UTC-11",
      "Name": "(UTC-11:00) Coordinated Universal Time-11"
    },
    {
      "Id": "Aleutian Standard Time",
      "Name": "(UTC-10:00) Aleutian Islands"
    },
    {
      "Id": "Hawaiian Standard Time",
      "Name": "(UTC-10:00) Hawaii"
    },
    {
      "Id": "Marquesas Standard Time",
      "Name": "(UTC-09:30) Marquesas Islands"
    },
    {
      "Id": "Alaskan Standard Time",
      "Name": "(UTC-09:00) Alaska"
    },
    {
      "Id": "UTC-09",
      "Name": "(UTC-09:00) Coordinated Universal Time-09"
    },
    {
      "Id": "Pacific Standard Time (Mexico)",
      "Name": "(UTC-08:00) Baja California"
    },
    {
      "Id": "UTC-08",
      "Name": "(UTC-08:00) Coordinated Universal Time-08"
    },
    {
      "Id": "Pacific Standard Time",
      "Name": "(UTC-08:00) Pacific Time (US & Canada)"
    },
    {
      "Id": "US Mountain Standard Time",
      "Name": "(UTC-07:00) Arizona"
    },
    {
      "Id": "Mountain Standard Time (Mexico)",
      "Name": "(UTC-07:00) Chihuahua, La Paz, Mazatlan"
    },
    {
      "Id": "Mountain Standard Time",
      "Name": "(UTC-07:00) Mountain Time (US & Canada)"
    },
    {
      "Id": "Central America Standard Time",
      "Name": "(UTC-06:00) Central America"
    },
    {
      "Id": "Central Standard Time",
      "Name": "(UTC-06:00) Central Time (US & Canada)"
    },
    {
      "Id": "Easter Island Standard Time",
      "Name": "(UTC-06:00) Easter Island"
    },
    {
      "Id": "Central Standard Time (Mexico)",
      "Name": "(UTC-06:00) Guadalajara, Mexico City, Monterrey"
    },
    {
      "Id": "Canada Central Standard Time",
      "Name": "(UTC-06:00) Saskatchewan"
    },
    {
      "Id": "SA Pacific Standard Time",
      "Name": "(UTC-05:00) Bogota, Lima, Quito, Rio Branco"
    },
    {
      "Id": "Eastern Standard Time (Mexico)",
      "Name": "(UTC-05:00) Chetumal"
    },
    {
      "Id": "Eastern Standard Time",
      "Name": "(UTC-05:00) Eastern Time (US & Canada)"
    },
    {
      "Id": "Haiti Standard Time",
      "Name": "(UTC-05:00) Haiti"
    },
    {
      "Id": "Cuba Standard Time",
      "Name": "(UTC-05:00) Havana"
    },
    {
      "Id": "US Eastern Standard Time",
      "Name": "(UTC-05:00) Indiana (East)"
    },
    {
      "Id": "Paraguay Standard Time",
      "Name": "(UTC-04:00) Asuncion"
    },
    {
      "Id": "Atlantic Standard Time",
      "Name": "(UTC-04:00) Atlantic Time (Canada)"
    },
    {
      "Id": "Venezuela Standard Time",
      "Name": "(UTC-04:00) Caracas"
    },
    {
      "Id": "Central Brazilian Standard Time",
      "Name": "(UTC-04:00) Cuiaba"
    },
    {
      "Id": "SA Western Standard Time",
      "Name": "(UTC-04:00) Georgetown, La Paz, Manaus, San Juan"
    },
    {
      "Id": "Pacific SA Standard Time",
      "Name": "(UTC-04:00) Santiago"
    },
    {
      "Id": "Turks And Caicos Standard Time",
      "Name": "(UTC-04:00) Turks and Caicos"
    },
    {
      "Id": "Newfoundland Standard Time",
      "Name": "(UTC-03:30) Newfoundland"
    },
    {
      "Id": "Tocantins Standard Time",
      "Name": "(UTC-03:00) Araguaina"
    },
    {
      "Id": "E. South America Standard Time",
      "Name": "(UTC-03:00) Brasilia"
    },
    {
      "Id": "SA Eastern Standard Time",
      "Name": "(UTC-03:00) Cayenne, Fortaleza"
    },
    {
      "Id": "Argentina Standard Time",
      "Name": "(UTC-03:00) City of Buenos Aires"
    },
    {
      "Id": "Greenland Standard Time",
      "Name": "(UTC-03:00) Greenland"
    },
    {
      "Id": "Montevideo Standard Time",
      "Name": "(UTC-03:00) Montevideo"
    },
    {
      "Id": "Saint Pierre Standard Time",
      "Name": "(UTC-03:00) Saint Pierre and Miquelon"
    },
    {
      "Id": "Bahia Standard Time",
      "Name": "(UTC-03:00) Salvador"
    },
    {
      "Id": "UTC-02",
      "Name": "(UTC-02:00) Coordinated Universal Time-02"
    },
    {
      "Id": "Mid-Atlantic Standard Time",
      "Name": "(UTC-02:00) Mid-Atlantic - Old"
    },
    {
      "Id": "Azores Standard Time",
      "Name": "(UTC-01:00) Azores"
    },
    {
      "Id": "Cape Verde Standard Time",
      "Name": "(UTC-01:00) Cabo Verde Is."
    },
    {
      "Id": "UTC",
      "Name": "(UTC) Coordinated Universal Time"
    },
    {
      "Id": "Morocco Standard Time",
      "Name": "(UTC+00:00) Casablanca"
    },
    {
      "Id": "GMT Standard Time",
      "Name": "(UTC+00:00) Dublin, Edinburgh, Lisbon, London"
    },
    {
      "Id": "Greenwich Standard Time",
      "Name": "(UTC+00:00) Monrovia, Reykjavik"
    },
    {
      "Id": "W. Europe Standard Time",
      "Name": "(UTC+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna"
    },
    {
      "Id": "Central Europe Standard Time",
      "Name": "(UTC+01:00) Belgrade, Bratislava, Budapest, Ljubljana, Prague"
    },
    {
      "Id": "Romance Standard Time",
      "Name": "(UTC+01:00) Brussels, Copenhagen, Madrid, Paris"
    },
    {
      "Id": "Central European Standard Time",
      "Name": "(UTC+01:00) Sarajevo, Skopje, Warsaw, Zagreb"
    },
    {
      "Id": "W. Central Africa Standard Time",
      "Name": "(UTC+01:00) West Central Africa"
    },
    {
      "Id": "Namibia Standard Time",
      "Name": "(UTC+01:00) Windhoek"
    },
    {
      "Id": "Jordan Standard Time",
      "Name": "(UTC+02:00) Amman"
    },
    {
      "Id": "GTB Standard Time",
      "Name": "(UTC+02:00) Athens, Bucharest"
    },
    {
      "Id": "Middle East Standard Time",
      "Name": "(UTC+02:00) Beirut"
    },
    {
      "Id": "Egypt Standard Time",
      "Name": "(UTC+02:00) Cairo"
    },
    {
      "Id": "E. Europe Standard Time",
      "Name": "(UTC+02:00) Chisinau"
    },
    {
      "Id": "Syria Standard Time",
      "Name": "(UTC+02:00) Damascus"
    },
    {
      "Id": "West Bank Standard Time",
      "Name": "(UTC+02:00) Gaza, Hebron"
    },
    {
      "Id": "South Africa Standard Time",
      "Name": "(UTC+02:00) Harare, Pretoria"
    },
    {
      "Id": "FLE Standard Time",
      "Name": "(UTC+02:00) Helsinki, Kyiv, Riga, Sofia, Tallinn, Vilnius"
    },
    {
      "Id": "Turkey Standard Time",
      "Name": "(UTC+02:00) Istanbul"
    },
    {
      "Id": "Israel Standard Time",
      "Name": "(UTC+02:00) Jerusalem"
    },
    {
      "Id": "Kaliningrad Standard Time",
      "Name": "(UTC+02:00) Kaliningrad"
    },
    {
      "Id": "Libya Standard Time",
      "Name": "(UTC+02:00) Tripoli"
    },
    {
      "Id": "Arabic Standard Time",
      "Name": "(UTC+03:00) Baghdad"
    },
    {
      "Id": "Arab Standard Time",
      "Name": "(UTC+03:00) Kuwait, Riyadh"
    },
    {
      "Id": "Belarus Standard Time",
      "Name": "(UTC+03:00) Minsk"
    },
    {
      "Id": "Russian Standard Time",
      "Name": "(UTC+03:00) Moscow, St. Petersburg, Volgograd"
    },
    {
      "Id": "E. Africa Standard Time",
      "Name": "(UTC+03:00) Nairobi"
    },
    {
      "Id": "Iran Standard Time",
      "Name": "(UTC+03:30) Tehran"
    },
    {
      "Id": "Arabian Standard Time",
      "Name": "(UTC+04:00) Abu Dhabi, Muscat"
    },
    {
      "Id": "Astrakhan Standard Time",
      "Name": "(UTC+04:00) Astrakhan, Ulyanovsk"
    },
    {
      "Id": "Azerbaijan Standard Time",
      "Name": "(UTC+04:00) Baku"
    },
    {
      "Id": "Russia Time Zone 3",
      "Name": "(UTC+04:00) Izhevsk, Samara"
    },
    {
      "Id": "Mauritius Standard Time",
      "Name": "(UTC+04:00) Port Louis"
    },
    {
      "Id": "Georgian Standard Time",
      "Name": "(UTC+04:00) Tbilisi"
    },
    {
      "Id": "Caucasus Standard Time",
      "Name": "(UTC+04:00) Yerevan"
    },
    {
      "Id": "Afghanistan Standard Time",
      "Name": "(UTC+04:30) Kabul"
    },
    {
      "Id": "West Asia Standard Time",
      "Name": "(UTC+05:00) Ashgabat, Tashkent"
    },
    {
      "Id": "Ekaterinburg Standard Time",
      "Name": "(UTC+05:00) Ekaterinburg"
    },
    {
      "Id": "Pakistan Standard Time",
      "Name": "(UTC+05:00) Islamabad, Karachi"
    },
    {
      "Id": "India Standard Time",
      "Name": "(UTC+05:30) Chennai, Kolkata, Mumbai, New Delhi"
    },
    {
      "Id": "Sri Lanka Standard Time",
      "Name": "(UTC+05:30) Sri Jayawardenepura"
    },
    {
      "Id": "Nepal Standard Time",
      "Name": "(UTC+05:45) Kathmandu"
    },
    {
      "Id": "Central Asia Standard Time",
      "Name": "(UTC+06:00) Astana"
    },
    {
      "Id": "Bangladesh Standard Time",
      "Name": "(UTC+06:00) Dhaka"
    },
    {
      "Id": "N. Central Asia Standard Time",
      "Name": "(UTC+06:00) Novosibirsk"
    },
    {
      "Id": "Myanmar Standard Time",
      "Name": "(UTC+06:30) Yangon (Rangoon)"
    },
    {
      "Id": "SE Asia Standard Time",
      "Name": "(UTC+07:00) Bangkok, Hanoi, Jakarta"
    },
    {
      "Id": "Altai Standard Time",
      "Name": "(UTC+07:00) Barnaul, Gorno-Altaysk"
    },
    {
      "Id": "W. Mongolia Standard Time",
      "Name": "(UTC+07:00) Hovd"
    },
    {
      "Id": "North Asia Standard Time",
      "Name": "(UTC+07:00) Krasnoyarsk"
    },
    {
      "Id": "Tomsk Standard Time",
      "Name": "(UTC+07:00) Tomsk"
    },
    {
      "Id": "China Standard Time",
      "Name": "(UTC+08:00) Beijing, Chongqing, Hong Kong, Urumqi"
    },
    {
      "Id": "North Asia East Standard Time",
      "Name": "(UTC+08:00) Irkutsk"
    },
    {
      "Id": "Singapore Standard Time",
      "Name": "(UTC+08:00) Kuala Lumpur, Singapore"
    },
    {
      "Id": "W. Australia Standard Time",
      "Name": "(UTC+08:00) Perth"
    },
    {
      "Id": "Taipei Standard Time",
      "Name": "(UTC+08:00) Taipei"
    },
    {
      "Id": "Ulaanbaatar Standard Time",
      "Name": "(UTC+08:00) Ulaanbaatar"
    },
    {
      "Id": "North Korea Standard Time",
      "Name": "(UTC+08:30) Pyongyang"
    },
    {
      "Id": "Aus Central W. Standard Time",
      "Name": "(UTC+08:45) Eucla"
    },
    {
      "Id": "Transbaikal Standard Time",
      "Name": "(UTC+09:00) Chita"
    },
    {
      "Id": "Tokyo Standard Time",
      "Name": "(UTC+09:00) Osaka, Sapporo, Tokyo"
    },
    {
      "Id": "Korea Standard Time",
      "Name": "(UTC+09:00) Seoul"
    },
    {
      "Id": "Yakutsk Standard Time",
      "Name": "(UTC+09:00) Yakutsk"
    },
    {
      "Id": "Cen. Australia Standard Time",
      "Name": "(UTC+09:30) Adelaide"
    },
    {
      "Id": "AUS Central Standard Time",
      "Name": "(UTC+09:30) Darwin"
    },
    {
      "Id": "E. Australia Standard Time",
      "Name": "(UTC+10:00) Brisbane"
    },
    {
      "Id": "AUS Eastern Standard Time",
      "Name": "(UTC+10:00) Canberra, Melbourne, Sydney"
    },
    {
      "Id": "West Pacific Standard Time",
      "Name": "(UTC+10:00) Guam, Port Moresby"
    },
    {
      "Id": "Tasmania Standard Time",
      "Name": "(UTC+10:00) Hobart"
    },
    {
      "Id": "Vladivostok Standard Time",
      "Name": "(UTC+10:00) Vladivostok"
    },
    {
      "Id": "Lord Howe Standard Time",
      "Name": "(UTC+10:30) Lord Howe Island"
    },
    {
      "Id": "Bougainville Standard Time",
      "Name": "(UTC+11:00) Bougainville Island"
    },
    {
      "Id": "Russia Time Zone 10",
      "Name": "(UTC+11:00) Chokurdakh"
    },
    {
      "Id": "Magadan Standard Time",
      "Name": "(UTC+11:00) Magadan"
    },
    {
      "Id": "Norfolk Standard Time",
      "Name": "(UTC+11:00) Norfolk Island"
  },
    {
      "Id": "Sakhalin Standard Time",
      "Name": "(UTC+11:00) Sakhalin"
    },
    {
      "Id": "Central Pacific Standard Time",
      "Name": "(UTC+11:00) Solomon Is., New Caledonia"
    },
    {
      "Id": "Russia Time Zone 11",
      "Name": "(UTC+12:00) Anadyr, Petropavlovsk-Kamchatsky"
    },
    {
      "Id": "New Zealand Standard Time",
      "Name": "(UTC+12:00) Auckland, Wellington"
    },
    {
      "Id": "UTC+12",
      "Name": "(UTC+12:00) Coordinated Universal Time+12"
    },
    {
      "Id": "Fiji Standard Time",
      "Name": "(UTC+12:00) Fiji"
    },
    {
      "Id": "Kamchatka Standard Time",
      "Name": "(UTC+12:00) Petropavlovsk-Kamchatsky - Old"
    },
    {
      "Id": "Chatham Islands Standard Time",
      "Name": "(UTC+12:45) Chatham Islands"
    },
    {
      "Id": "Tonga Standard Time",
      "Name": "(UTC+13:00) Nuku'alofa"
    },
    {
      "Id": "Samoa Standard Time",
      "Name": "(UTC+13:00) Samoa"
    },
    {
      "Id": "Line Islands Standard Time",
      "Name": "(UTC+14:00) Kiritimati Island"
    }
  ]



  

**********************


