# NSData, NSString, char* 데이터 변환

**NSString to char***

~~~objc
// dataString -> NSString 
char *buffer = [dataString UTF8String];
~~~

**char* to NSString**

~~~objc
// buffer -> char*
NSString *dataString = [NSString stringWithUTF8String: buffer]; // -> 1번째 방법
NSString *dataString = [NSString stringWithFormat:@"%s", buffer]; // -> 2번째 방법
~~~

**NSData to char***

~~~objc
// data -> NSData
const char *buffer = (const char*)[data bytes];
~~~

**char* to NSData**

~~~~objc
// buffer -> char*
// size -> int
NSData *data = [NSData dataWithBytes:buffer length:size];
~~~~

**NSData to NSString**

~~~objc
// data -> NSData
NSString *dataString = [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
~~~

**NSString to NSData**

~~~objc
// dataString -> NSString
NSData *data = [dataString dataUsingEncoding:NSUTF8StringEncoding];
~~~

<br /><br />

# Encoding issue

NSString <-> NSData 서로 변환하는 과정에서 변환 후에 length 값이 0으로 떨어질때가 있다.

NSUTF8StringEncoding 데이터에 따라 옵션이 잘못되었을 수도 있다. NSASCIIStringEncoding로 변경하니 제대로 나왔다.

~~~~objc
// 옵션 종류
enum {
   NSASCIIStringEncoding = 1,    //Western (ASCII) US-ASCII
   NSNEXTSTEPStringEncoding = 2,  //Western (ASCII) US-ASCII
   NSJapaneseEUCStringEncoding = 3,  //Japanese (EUC) EUC-JP
   NSUTF8StringEncoding = 4,   //Unicode (UTF-8) UTF-8
   NSISOLatin1StringEncoding = 5,  //Western (ISO Latin 1) ISO-8859-1
   NSSymbolStringEncoding = 6,   //Symbol (Mac OS) X-MAC-SYMBOL
   NSNonLossyASCIIStringEncoding = 7,  //Non-lossy ASCII
   NSShiftJISStringEncoding = 8,  //Japanese (Windows, DOS) CP932
   NSISOLatin2StringEncoding = 9,  //Central European (ISO Latin 2) ISO-8859-2
   NSUnicodeStringEncoding = 10,  //Unicode (UTF-16) UTF-16
   NSWindowsCP1251StringEncoding = 11,  //Cyrillic (Windows) WINDOWS-1251
   NSWindowsCP1252StringEncoding = 12,  //Western (Windows Latin 1) WINDOWS-1252
   NSWindowsCP1253StringEncoding = 13,  //Greek (Windows) WINDOWS-1253
   NSWindowsCP1254StringEncoding = 14,  //Turkish (Windows Latin 5) WINDOWS-1254
   NSWindowsCP1250StringEncoding = 15,  //Central European (Windows Latin 2) WINDOWS-1250
   NSISO2022JPStringEncoding = 21,  //Japanese (ISO 2022-JP) ISO-2022-JP
   NSMacOSRomanStringEncoding = 30,  //Western (Mac OS Roman) MACINTOSH
   NSUTF16StringEncoding = NSUnicodeStringEncoding,
   NSUTF16BigEndianStringEncoding = 0x90000100,  
   NSUTF16LittleEndianStringEncoding = 0x94000100,
   NSUTF32StringEncoding = 0x8c000100,
   NSUTF32BigEndianStringEncoding = 0x98000100,
   NSUTF32LittleEndianStringEncoding = 0x9c000100,
   NSProprietaryStringEncoding = 65536
};
~~~~

