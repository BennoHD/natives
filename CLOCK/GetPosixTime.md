---
ns: CLOCK
---
## GET_POSIX_TIME

```c
// 0xDA488F299A5B164E 0xE15A5281
void GET_POSIX_TIME(int* year, int* month, int* day, int* hour, int* minute, int* second);
```

```
Gets system time as year, month, day, hour, minute and second.  
Example usage:  
	int year;  
	int month;  
	int day;  
	int hour;  
	int minute;  
	int second;  
	TIME::GET_POSIX_TIME(&year, &month, &day, &hour, &minute, &second);  
	
	
--------------------------------------------
In Lua, this wont work, since it returns C# struct, these are functions that you can use to get time as os.date server-side is:

local function GetIntFromBlob(b, s, o)
	r = 0
	for i=1,s,1 do
		r = r | (string.byte(b,o+i)<<(i-1)*8)
	end
	return r
end

function UnixDate(epoch)
	blob = '\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0'
	retval = Citizen.InvokeNative(0xAC97AF97FA68E5D5, epoch, blob, Citizen.ReturnResultAnyway())
	year = GetIntFromBlob(blob,8,0)
	month = GetIntFromBlob(blob,8,8)
	day = GetIntFromBlob(blob,8,16)
	hour = GetIntFromBlob(blob,8,24)
	minute = GetIntFromBlob(blob,8,32)
	second = GetIntFromBlob(blob,8,40)
	return string.format("%s-%s-%s %s:%s:%s", year,month,day,hour,minute,second)
end

-- Source: http://www.kronzky.info/fivemwiki/index.php?title=GetDateAndTimeFromUnixEpoch with a bit of editing

```

## Parameters
* **year**: 
* **month**: 
* **day**: 
* **hour**: 
* **minute**: 
* **second**: 

