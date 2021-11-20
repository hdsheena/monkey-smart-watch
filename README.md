# monkey-smart-watch
reverse engineering attempt for Anex Monkey SmartWatch

What I know so far:
BLE Chip: Pixart Par2801 https://fccid.io/2AIPB-PAJ2801UA-40/User-Manual/Users-Manual-3083972

Heart rate and BP data:
Bytes 4-10 are either:
244000150b1414 - blood pressure?
240700150b1401 - not bp. maybe hr?

| Command  | first 3 bytes | Last 4 bytes
| ------------- | ------------- | ------
| Ring phone from watch  | aeba38  | 80010001
| Ring watch from phone  | ae9918 | 80010000
| Raise to wake on |  ae7c70 | 08010003
| Raise to wake off |  ae7168 | 08010000


Wireshark logs source data:
```
14752	6698.671805	f8:26:94:24:7f:00 (ThinFit-36)	Google_0d:c2:6c (Pixel 5)	ATT	19	aeba3880010001	Nov 20, 2021 12:21:44.539689000 PST	tried to ring phone from watch	Rcvd Handle Value Notification, Handle: 0x0022 (Unknown: Unknown)
14703	6684.496846	f8:26:94:24:7f:00 (ThinFit-36)	Google_0d:c2:6c (Pixel 5)	ATT	19	aeb23080010001	Nov 20, 2021 12:21:30.364730000 PST	tried to ring phone from watch	Rcvd Handle Value Notification, Handle: 0x0022 (Unknown: Unknown)
14702	6671.040903	f8:26:94:24:7f:00 (ThinFit-36)	Google_0d:c2:6c (Pixel 5)	ATT	19	aeaa2880010001	Nov 20, 2021 12:21:16.908787000 PST	tried to ring phone from watch	Rcvd Handle Value Notification, Handle: 0x0022 (Unknown: Unknown)
14701	6662.582318	f8:26:94:24:7f:00 (ThinFit-36)	Google_0d:c2:6c (Pixel 5)	ATT	19	aea22080010001	Nov 20, 2021 12:21:08.450202000 PST	tried to ring phone from watch	Rcvd Handle Value Notification, Handle: 0x0022 (Unknown: Unknown)
14700	6659.252070	f8:26:94:24:7f:00 (ThinFit-36)	Google_0d:c2:6c (Pixel 5)	ATT	19	ae9a1880010001	Nov 20, 2021 12:21:05.119954000 PST	tried to ring phone from watch	Rcvd Handle Value Notification, Handle: 0x0022 (Unknown: Unknown)
14679	6622.487321	Google_0d:c2:6c (Pixel 5)	f8:26:94:24:7f:00 (ThinFit-36)	ATT	19	ae991880010000	Nov 20, 2021 12:20:28.355205000 PST	Phone triggered find-watch	Sent Write Request, Handle: 0x0020 (Unknown: Unknown)
14699	6654.975853	f8:26:94:24:7f:00 (ThinFit-36)	Google_0d:c2:6c (Pixel 5)	ATT	19	ae921080010001	Nov 20, 2021 12:21:00.843737000 PST	tried to ring phone from watch	Rcvd Handle Value Notification, Handle: 0x0022 (Unknown: Unknown)
14630	6598.572245	Google_0d:c2:6c (Pixel 5)	f8:26:94:24:7f:00 (ThinFit-36)	ATT	19	ae911080010000	Nov 20, 2021 12:20:04.440129000 PST	Phone triggered find-watch	Sent Write Request, Handle: 0x0020 (Unknown: Unknown)
14698	6651.152522	f8:26:94:24:7f:00 (ThinFit-36)	Google_0d:c2:6c (Pixel 5)	ATT	19	ae8a0880010001	Nov 20, 2021 12:20:57.020406000 PST	tried to ring phone from watch	Rcvd Handle Value Notification, Handle: 0x0022 (Unknown: Unknown)
14183	6570.726858	Google_0d:c2:6c (Pixel 5)	f8:26:94:24:7f:00 (ThinFit-36)	ATT	19	ae890880010000	Nov 20, 2021 12:19:36.594742000 PST	Phone triggered find-watch	Sent Write Request, Handle: 0x0020 (Unknown: Unknown)
15319	6821.139487	Google_0d:c2:6c (Pixel 5)	f8:26:94:24:7f:00 (ThinFit-36)	ATT	19	ae7c7008010003	Nov 20, 2021 12:23:47.007371000 PST	raise to wake on	Sent Write Request, Handle: 0x0020 (Unknown: Unknown)
15310	6815.775333	Google_0d:c2:6c (Pixel 5)	f8:26:94:24:7f:00 (ThinFit-36)	ATT	19	ae716808010000	Nov 20, 2021 12:23:41.643217000 PST	raise to wake off	Sent Write Request, Handle: 0x0020 (Unknown: Unknown)
15297	6804.748740	Google_0d:c2:6c (Pixel 5)	f8:26:94:24:7f:00 (ThinFit-36)	ATT	19	ae6c6008010003	Nov 20, 2021 12:23:30.616624000 PST	raise to wake on	Sent Write Request, Handle: 0x0020 (Unknown: Unknown)
15289	6791.288355	Google_0d:c2:6c (Pixel 5)	f8:26:94:24:7f:00 (ThinFit-36)	ATT	19	ae615808010000	Nov 20, 2021 12:23:17.156239000 PST	raise to wake off	Sent Write Request, Handle: 0x0020 (Unknown: Unknown)
14856	6722.611389	Google_0d:c2:6c (Pixel 5)	f8:26:94:24:7f:00 (ThinFit-36)	ATT	20	ae61302d02000101	Nov 20, 2021 12:22:08.479273000 PST	ask watch for heartrate	Sent Write Request, Handle: 0x0020 (Unknown: Unknown)
```


https://docs.google.com/spreadsheets/d/1Ple4YaWk5sm64zbLxi8QcCqBqfklNmR-aAzLxdn_XLo/edit#gid=0
