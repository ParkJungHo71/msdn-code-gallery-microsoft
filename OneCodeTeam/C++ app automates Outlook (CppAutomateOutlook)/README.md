# C++ app automates Outlook (CppAutomateOutlook)
## Requires
- Visual Studio 2008
## License
- Apache License, Version 2.0
## Technologies
- Office
## Topics
- Outlook
- Automation
## Updated
- 05/05/2011
## Description

<p style="font-family:Courier New"></p>
<h2>CONSOLE APPLICATION : CppAutomateOutlook Project Overview</h2>
<p style="font-family:Courier New"></p>
<h3>Summary:</h3>
<p style="font-family:Courier New"><br>
The CppAutomateOutlook example demonstrates how to write VC&#43;&#43; code to <br>
automate Microsoft Outlook to log on with your profile, enumerate contacts, <br>
send a mail, log off, close the Microsoft Outlook application and then clean <br>
up unmanaged COM resources. <br>
<br>
There are three basic ways you can write VC&#43;&#43; automation codes:<br>
<br>
1. Automating Outlook using the #import directive and smart pointers <br>
<br>
The code in Solution1.h/cpp demonstrates the use of #import to automate<br>
Outlook. #import (<a target="_blank" href="http://msdn.microsoft.com/en-us/library/8etzzkb6.aspx),">http://msdn.microsoft.com/en-us/library/8etzzkb6.aspx),</a> a
<br>
new directive that became available with Visual C&#43;&#43; 5.0, creates VC&#43;&#43; &quot;smart
<br>
pointers&quot; from a specified type library. It is very powerful, but often not <br>
recommended because of reference-counting problems that typically occur when <br>
used with the Microsoft Office applications. Unlike the direct API approach <br>
in Solution2.h/cpp, smart pointers enable us to benefit from the type info to <br>
early/late bind the object. #import takes care of adding the messy guids to <br>
the project and the COM APIs are encapsulated in custom classes that the <br>
#import directive generates.<br>
<br>
2. Automating Outlook using C&#43;&#43; and the COM APIs<br>
<br>
The code in Solution2.h/cpp demontrates the use of C/C&#43;&#43; and the COM APIs to <br>
automate Outlook. The raw automation is much more difficult, but it is &nbsp;<br>
sometimes necessary to avoid the overhead with MFC, or problems with #import. <br>
Basically, you work with such APIs as CoCreateInstance(), and COM interfaces <br>
such as IDispatch and IUnknown.<br>
<br>
3. Automating Outlook with MFC<br>
<br>
With MFC, Visual C&#43;&#43; Class Wizard can generate &quot;wrapper classes&quot; from the
<br>
type libraries. These classes simplify the use of the COM servers. Automating <br>
Outlook with MFC is not covered in this sample.<br>
<br>
</p>
<h3>Prerequisite:</h3>
<p style="font-family:Courier New"><br>
You must run this code sample on a computer that has Microsoft Outlook 2007 <br>
installed.<br>
<br>
</p>
<h3>Demo:</h3>
<p style="font-family:Courier New"><br>
The following steps walk through a demonstration of the Outlook automation <br>
sample that starts a Microsoft Outlook instance, logs on with your profile, <br>
enumerates the contact items, creates and sends a new mail item, logs off and <br>
quits the Microsoft Outlook application cleanly.<br>
<br>
Step1. After you successfully build the sample project in Visual Studio 2008, <br>
you will get the application: CppAutomateOutlook.exe.<br>
<br>
Step2. Open Windows Task Manager (Ctrl&#43;Shift&#43;Esc) to confirm that no <br>
outlook.exe is running. <br>
<br>
Step3. Run the application. It should print the following content in the <br>
console window if no error is thrown.<br>
<br>
&nbsp;Outlook.Application is started<br>
&nbsp;User logs on ...<br>
&nbsp;Please press ENTER to continue when Outlook is ready.<br>
<br>
Outlook would ask you to input your profile and password. When Outlook is <br>
ready, press ENTER in the console window of CppAutomateOutlook. The <br>
application will then enumerate your contacts and print the contacts:<br>
<br>
&nbsp;Enumerate the contact items<br>
&nbsp;&lt;the email address of your contacts and the name of your discussion lists&gt;<br>
<br>
Next, CppAutomateOutlook automates Outlook to create and display or send a <br>
new mail item. <br>
<br>
&nbsp;Create and send a new mail item<br>
<br>
In the new mail item, the To line is set as codefxf@microsoft.com, which is <br>
the feedback channel of All-In-One Code Framework. The Subject is set to <br>
&quot;Feedback of All-In-One Code Framework&quot; and the email body shows &quot;Feedback:&quot;
<br>
in bold.<br>
<br>
After you input your feedback and click the Send button, the mail item is <br>
sent and CppAutomateOutlook automates Outlook to log off the current profile <br>
and quit itself.<br>
<br>
&nbsp;Log off and quit the Outlook application<br>
<br>
Step4. In Windows Task Manager, confirm that the outlook.exe process does not <br>
exist, i.e. the Microsoft Outlook intance was closed and cleaned up properly.<br>
<br>
</p>
<h3>Project Relation:</h3>
<p style="font-family:Courier New"><br>
CppAutomateOutlook - CSAutomateOutlook - VBAutomateOutlook<br>
<br>
These examples automate Microsoft Outlook to do the same thing in different <br>
programming languages.<br>
<br>
</p>
<h3>Creation:</h3>
<p style="font-family:Courier New"><br>
A. Automating Outlook using the #import directive and smart pointers <br>
(Solution1.h/cpp)<br>
<br>
Step1. Import the type library of the target COM server using the #import <br>
directive. <br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;#import &quot;libid:2DF8D04C-5BFA-101B-BDE5-00AA0044DE52&quot; \<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rename(&quot;RGB&quot;, &quot;MSORGB&quot;) \<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rename(&quot;DocumentProperties&quot;, &quot;MSODocumentProperties&quot;)<br>
&nbsp;&nbsp;&nbsp;&nbsp;// [-or-]<br>
&nbsp;&nbsp;&nbsp;&nbsp;//#import &quot;C:\\Program Files\\Common Files\\Microsoft Shared\\OFFICE12\\MSO.DLL&quot; \<br>
&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;&nbsp;&nbsp;&nbsp;rename(&quot;RGB&quot;, &quot;MSORGB&quot;) \<br>
&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;&nbsp;&nbsp;&nbsp;rename(&quot;DocumentProperties&quot;, &quot;MSODocumentProperties&quot;)<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;using namespace Office;<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;#import &quot;progid:Outlook.Application&quot; \<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rename(&quot;CopyFile&quot;, &quot;OutlookCopyFile&quot;) \<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rename(&quot;PlaySound&quot;, &quot;OutlookPlaySound&quot;)<br>
&nbsp;&nbsp;&nbsp;&nbsp;// [-or-]<br>
&nbsp;&nbsp;&nbsp;&nbsp;//#import &quot;libid:00062FFF-0000-0000-C000-000000000046&quot; \<br>
&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;&nbsp;&nbsp;&nbsp;rename(&quot;CopyFile&quot;, &quot;OutlookCopyFile&quot;) \<br>
&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;&nbsp;&nbsp;&nbsp;rename(&quot;PlaySound&quot;, &quot;OutlookPlaySound&quot;)<br>
&nbsp;&nbsp;&nbsp;&nbsp;// [-or-]<br>
&nbsp;&nbsp;&nbsp;&nbsp;//#import &quot;C:\\Program Files\\Microsoft Office\\Office12\\MSOUTL.OLB&quot;&nbsp;&nbsp;&nbsp;&nbsp;\<br>
&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;&nbsp;&nbsp;&nbsp;rename(&quot;CopyFile&quot;, &quot;OutlookCopyFile&quot;) \<br>
&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;&nbsp;&nbsp;&nbsp;rename(&quot;PlaySound&quot;, &quot;OutlookPlaySound&quot;)<br>
<br>
Step2. Build the project. If the build is successful, the compiler generates <br>
the .tlh and .tli files that encapsulate the COM server based on the type <br>
library specified in the #import directive. It serves as a class wrapper we<br>
can now use to create the COM class and access its properties, methods, etc.<br>
<br>
Step3. Initializes the COM library on the current thread and identifies the <br>
concurrency model as single-thread apartment (STA) by calling CoInitializeEx, <br>
or CoInitialize.<br>
<br>
Step4. Create the Outlook.Application COM object using the smart pointer. The <br>
class name is the original interface name (i.e. Outlook::_Application) with a <br>
&quot;Ptr&quot; suffix. We can use either the constructor of the smart pointer class or
<br>
its CreateInstance method to create the COM object.<br>
<br>
Step5. Automate the Outlook COM object through the smart pointers. In this <br>
example, you can find the basic operations in Outlook automation like <br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;Start Microsoft Outlook and log on with your profile.<br>
&nbsp;&nbsp;&nbsp;&nbsp;Enumerate the contact items.<br>
&nbsp;&nbsp;&nbsp;&nbsp;Create and display/send a new mail item.<br>
&nbsp;&nbsp;&nbsp;&nbsp;User logs off.<br>
<br>
Step6. Quit the Outlook application. (i.e. Application.Quit())<br>
<br>
Step7. It is said that the smart pointers are released automatically, so we <br>
do not need to manually release the COM objects.<br>
<br>
Step8. It is necessary to catch the COM errors if the type library was &nbsp;<br>
imported without raw_interfaces_only and when the raw interfaces <br>
(e.g. raw_Quit) are not used. For example:<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;#import &quot;XXXX.tlb&quot;<br>
&nbsp;&nbsp;&nbsp;&nbsp;try<br>
&nbsp;&nbsp;&nbsp;&nbsp;{<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;spOutookApp-&gt;Quit();<br>
&nbsp;&nbsp;&nbsp;&nbsp;}<br>
&nbsp;&nbsp;&nbsp;&nbsp;catch (_com_error &err)<br>
&nbsp;&nbsp;&nbsp;&nbsp;{<br>
&nbsp;&nbsp;&nbsp;&nbsp;}<br>
<br>
Step9. Uninitialize COM for this thread by calling CoUninitialize.<br>
<br>
-----------------------------------------------------------------------------<br>
<br>
B. Automating Outlook using C&#43;&#43; and the COM APIs (Solution2.h/cpp)<br>
<br>
Step1. Add the automation helper function, AutoWrap.<br>
<br>
Step2. Initializes the COM library on the current thread and identifies the <br>
concurrency model as single-thread apartment (STA) by calling CoInitializeEx, <br>
or CoInitialize.<br>
<br>
Step3. Get CLSID of the Outlook COM server using the API CLSIDFromProgID.<br>
<br>
Step4. Start the Outlook COM server and get the IDispatch interface using &nbsp;<br>
the API CoCreateInstance.<br>
<br>
Step5. Automate the Outlook COM object with the help of AutoWrap. In this <br>
example, you can find the basic operations in Outlook automation like <br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;Start Microsoft Outlook and log on with your profile.<br>
&nbsp;&nbsp;&nbsp;&nbsp;Create and send a new mail item.<br>
&nbsp;&nbsp;&nbsp;&nbsp;User logs off.<br>
<br>
Step6. Quit the Outlook application. (i.e. Application.Quit())<br>
<br>
Step7. Release the COM objects.<br>
<br>
Step8. Uninitialize COM for this thread by calling CoUninitialize.<br>
<br>
</p>
<h3>References:</h3>
<p style="font-family:Courier New"><br>
MSDN: Outlook 2007 Developer Reference<br>
<a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb177050.aspx">http://msdn.microsoft.com/en-us/library/bb177050.aspx</a><br>
<br>
How to use an Outlook Object Model from Visual C&#43;&#43; by using a #import <br>
statement<br>
<a target="_blank" href="http://support.microsoft.com/kb/259298">http://support.microsoft.com/kb/259298</a><br>
<br>
Importing Type Libraries<br>
<a target="_blank" href="http://www.codeproject.com/KB/tips/importtlbs.aspx">http://www.codeproject.com/KB/tips/importtlbs.aspx</a><br>
<br>
<br>
</p>
<hr>
<div><a href="http://go.microsoft.com/?linkid=9759640" style="margin-top:3px"><img src="http://bit.ly/onecodelogo">
</a></div>
