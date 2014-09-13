SLPhant: a Second Life/OpenSim Phant Library.
Tested in both Second Life(tm) and OpenSim(tm).


With SLPhant you can...
* Clear All Data
* Add Data
* Get Data (in Supported Formats)
* Get Stats (in Supported Formats)
* Supported Formats [CSV, JSON, MySQL, PostgreSQL, ATOM]


To Test the Example:
1) Copy SLPhant_v1_0.lsl to a script in your own Prim and save.

2) Monitor chat (uses llOwnerSay) to see results.

3) View the data at https://data.sparkfun.com/streams/7JvgN1NbE5H2JwAvlza0 to see that it worked.


Usage in your own scripts:
1) Copy the upper half to your own script (above where it says "above this line")

2) Modify these two constants to use *YOUR* keys
   (the keys shown here are for a public stream only used for demonstration.)
	string sSLPHANT_PUBLIC_KEY  = "7JvgN1NbE5H2JwAvlza0";
	string sSLPHANT_PRIVATE_KEY = "mzqm6g6GNaS0q6D7RrNy";

3) If you're running your own Phant Server, modify the following constant
	string sSLPHANT_BASE_URL    = "https://data.sparkfun.com/";

4) Use of the following Functions is self explanitory to any self-respecting scripter...
	key SLPhant_Clear();
	key SLPhant_AddData(string sData);
	key SLPhant_RequestData(string sFormat);
	key SLPhant_RequestStats(string sFormat);

5) Results are returned when the http_response Event fires...
	http_response(key kRequestId, integer iStatus, list lMetadata, string sBody);


The only thing that may need explaining is the Formatting of the Data for SLPhant_AddData.
	It is *YOUR* responsibility to have sData in format "Field1=Value1&Field2=Value2..."
	Fields must be the valid names for YOUR stream.
	Values must be put thru llEscapeURL(sURL).
	Name/Value pairs must be separated by "&".

	For example (note use of llEscapeURL)...
		SLPhant_AddData(
			"avatarname="+llEscapeURL(llKey2Name(llGetOwner()))+
			"&id="+llEscapeURL(llGetOwner())+
			"&regionname="+llEscapeURL(llGetRegionName()));


Note that Phant sometimes messes up if accessed too fast; so I put a llSleep(1.0) in the loop (YMMV.)
