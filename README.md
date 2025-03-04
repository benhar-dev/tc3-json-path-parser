# tc3-json-path-parser

## Disclaimer

This is a personal guide not a peer reviewed journal or a sponsored publication. We make
no representations as to accuracy, completeness, correctness, suitability, or validity of any
information and will not be liable for any errors, omissions, or delays in this information or any
losses injuries, or damages arising from its display or use. All information is provided on an as
is basis. It is the reader’s responsibility to verify their own facts.

The views and opinions expressed in this guide are those of the authors and do not
necessarily reflect the official policy or position of any other agency, organization, employer or
company. Assumptions made in the analysis are not reflective of the position of any entity
other than the author(s) and, since we are critically thinking human beings, these views are
always subject to change, revision, and rethinking at any time. Please do not hold us to them
in perpetuity.

## Overview

This is a simple code snippet showing how to use the FB_JsonDomParser with path. There is no TwinCAT solution for this, only the snippet below.

## Getting Started

Start a new TwinCAT project and be sure to add the TC3_JsonXml library. Copy and paste the code below in to your main program.

```
PROGRAM MAIN
VAR
	// remember to make a string large enough to hold the json.
	jsonString : T_MAXSTRING :=
		'[
			  {
				"First": 4
			  },
			  {
				"Second": 12,
				"Third": [100, 200, 300],
				"Fourth": {
				  "a": true
				}
			  }
			]';

	triggered : BOOL;
	jsonParser : FB_JsonDomParser;
	jsonDocument : SJsonValue;
	jsonProperty : SJsonValue;
	value : DINT;
END_VAR

//

IF NOT triggered THEN
	jsonDocument := jsonParser.ParseDocument(jsonString);
	jsonProperty := jsonParser.FindMemberPath(jsonDocument, '#1/Third#2');
	value := jsonParser.GetInt(jsonProperty); // value = 300 (as arrays are zero indexed);
	triggered := TRUE;
END_IF
```

## Screenshot

![image](./docs/images/screenshot.png)

## Need more help?

Please visit http://beckhoff.com/ for further guides
