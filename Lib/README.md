## Easy Ini Class: Bug Workaround
**Source**: [AutoHotkey Forum - Conversation with Easy_Ini.ahk author](https://www.autohotkey.com/boards/viewtopic.php?f=6&t=5522)
>> **[user 1] wrote**: Great class, Verdlin!  
>>   
>> Do you still support it?  
>> ...  
>> So the section is still there but the contents of the next following section is transferred into it.  
>>   
>> So atm, it doesn't work with integer section names only. Can this be fixed?
>
>**[Aatoz(the author)](https://github.com/Aatoz) wrote**: Thanks, [user]! This is a [known bug](http://www.autohotkey.com/board/topic/94043-ordered-array/#entry607614). I've not been able to fix the bug because the code has been too complex for me to figure out.  
>  
>>**[user 2 wrote]**:I don't know if this is a good workaround for you, but you can add ".0" to the end of all your sections to get around this bug. Let me know if that's good enough. I could write a script for you to do this, but I think it's as simple as using Find/Replace in Notepad++ and replacing "]" with ".0]"  
>  
>Long term I'd like to code a solution to this bug, but it's tricky. I have a few ideas a may try in the next week or so.  

### CODE: 
```autohotkey
{
	sIni:="
		(LTrim
			[20150927234336.0]
			test=1
 
			[20150927234337.0]
			test=2

			[20150927234338.0]
			test=3
		)"
 
	vIni := class_EasyIni("test.ini", sIni)
	for sec, aData in vIni
		for k, v in aData
			s .= s == "" ? "[" sec "]`n" k "=" v : "`n[" sec "]`n" k "=" v

	vIni.DeleteSection("20150927234337.0")
	s :=

	for sec, aData in vIni
		for k, v in aData
			s .= s == "" ? "[" sec "]`n" k "=" v : "`n[" sec "]`n" k "=" v

	Msgbox % s

	return
}
```

### Output:  
```shell
[20150927234336.0]  
test=1  
[20150927234338.0]  
test=3
```
