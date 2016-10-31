---
title: Preprocessor Directives
author: windows-driver-content
description: Preprocessor Directives
MS-HAID:
- 'nt5gpd\_3ee60963-debd-4501-b2e8-33e0c0e8d47f.xml'
- 'print.preprocessor\_directives'
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 5731b159-c6f9-47a8-8eaa-a1b0b6c12132
keywords: ["GPD file entries WDK Unidrv , preprocessor directives", "preprocessor directives WDK GPD files", "parsing GPD file sections", "preprocessor symbols WDK GPD files"]
---

# Preprocessor Directives


## <a href="" id="ddk-preprocessor-directives-gg"></a>


GPD files can contain preprocessor directives, which can be used to control conditional parsing of sections within the GPD file. The following table describes the preprocessor directives that can be used in GPD files.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PreprocessorDirective</th>
<th>Definition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>*<strong>Define</strong>: <em>SymbolName</em></p></td>
<td><p>Defines a symbol.</p></td>
</tr>
<tr class="even">
<td><p>*<strong>Undefine</strong>: <em>SymbolName</em></p></td>
<td><p>Removes a previously defined symbol.</p></td>
</tr>
<tr class="odd">
<td><p>*<strong>Ifdef</strong> : <em>SymbolName</em></p></td>
<td><p>Indicates the beginning of a block of GPD file entries.</p>
<p>If the specified symbol is defined, the GPD file entries between this directive and the next *<strong>Ifdef</strong>, *<strong>Elseifdef</strong>, *<strong>Else</strong>, or *<strong>Endif</strong> directive are processed by the GPD parser.</p></td>
</tr>
<tr class="even">
<td><p>*<strong>Elseifdef</strong> : <em>SymbolName</em></p></td>
<td><p>If the specified symbol is defined, and the symbol specified by the previous *<strong>Ifdef</strong> or *<strong>Elseifdef</strong> directive is undefined, the GPD file entries between this directive and the next *<strong>Ifdef</strong>, *<strong>Elseifdef</strong>, *<strong>Else</strong>, or *<strong>Endif</strong> directive are processed by the GPD parser.</p></td>
</tr>
<tr class="odd">
<td><p>*<strong>Else</strong> :</p></td>
<td><p>If the symbol specified by the previous *<strong>Ifdef</strong> or *<strong>Elseifdef</strong> directive is undefined, the GPD file entries between this directive and the next *<strong>Ifdef</strong> or *<strong>Endif</strong> directive are processed by the GPD parser.</p></td>
</tr>
<tr class="even">
<td><p>*<strong>Endif</strong> :</p></td>
<td><p>Indicates the end of a block of GPD file entries.</p></td>
</tr>
<tr class="odd">
<td><p>*<strong>Include</strong> : &quot;<em>FileName</em>&quot;</p></td>
<td><p>Specifies the name of an additional GPD file. See [Using Multiple GPD Files in a Minidriver](using-multiple-gpd-files-in-a-minidriver.md).</p></td>
</tr>
<tr class="even">
<td><p>*<strong>SetPPPrefix</strong> : <em>PrefixString</em></p></td>
<td><p>Changes the prefix string prepended to preprocessor directives. See the <strong>Changing the Preprocessor Directive Prefix</strong> section.</p></td>
</tr>
</tbody>
</table>

 

Conditional preprocessor directives can be nested. At each nesting level, the sequence for using conditional preprocessor directives is as follows:

\***Ifdef**: *Symbol1* GPD file section

\***Elseifdef**: *Symbol2* GPD file section

\***Elseifdef**: *Symbol3* GPD file section

\***Elseifdef**: *Symbol4* GPD file section

...

\***Else**: GPD file section

\***Endif**:

For each \***Ifdef** directive used, \***Endif** is required. The \***Elseifdef** and \***Else** directives are optional. Each GPD file section can contain GPD file entries and, optionally, a nested sequence of conditional preprocessor directives.

All symbols defined using \***Define** remain defined until explicitly undefined using \***Undefine**.

The \***Include** directive allows you to specify the name of an additional GPD file. For more information, see [Using Multiple GPD Files in a Minidriver](using-multiple-gpd-files-in-a-minidriver.md).

Note that the \*IgnoreBlock GPD entry does not affect preprocessor directives, because the preprocessor executes before the GPD parser.

### <a href="" id="ddk-changing-the-preprocessor-directive-prefix-gg"></a>Changing the Preprocessor Directive Prefix

The \***SetPPPrefix** directive allows you to change the prefix used with preprocessor directives. That is, you can use this directive to replace the asterisk (\*) character that prepends the preprocessor directives with another character or string.

For example, if your GPD file contains the following directive:

```
*SetPPPrefix: #SpecialPrefix#
```

then the preprocessor stops searching for preprocessor directives that begin with **\*** and instead looks for directives beginning with **\#SpecialPrefix\#**. The following sequence temporarily changes the preprocessor prefix to **\#SpecialPrefix\#**, then restores it to **\***.

```
*SetPPPrefix: #SpecialPrefix#
#SpecialPrefix#Ifdef: WINNT_50
#SpecialPrefix#Include: "ExtraGPD.gpd"
#SpecialPrefix#Endif:
#SpecialPrefix#SetPPPrefix: *
```

The primary purpose of this feature is to allow GPD files written for future operating system versions to be compatible with Windows 2000. For example, suppose GPD files for a future version of the operating system can include GPD file entries that conflict with the asterisk-prefixed preprocessor directives supported by Windows 2000. By changing the prefix, a GPD file written for the future operating system version can also be used with Windows 2000. An example might be constructed as follows:

```
*Ifdef: WINNT_70
    *SetPPPrefix: #SpecialPrefix#
    *% Do special, OS-specific processing of
    *% GPD file entries that might conflict with
    *% asterisk-prefixed preprocessor directives.
    #SpecialPrefix#SetPPPrefix: *
*Endif:
```

Note that this technique only changes the prefix that the preprocessor looks for. Keywords recognized by the parser must always be preceded by an asterisk.

### <a href="" id="ddk-predefined-preprocessor-symbols-gg"></a>Predefined Preprocessor Symbols

Microsoft defines the following preprocessor symbols.

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Symbol</th>
<th>Where Defined</th>
<th>Definition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WINNT_51</p></td>
<td><p>GPD preprocessor for Windows XP</p></td>
<td><p>Environment is Windows XP.</p></td>
</tr>
<tr class="even">
<td><p>WINNT_50</p></td>
<td><p>GPD preprocessor for Windows XP and Windows 2000</p></td>
<td><p>Environment is Windows 2000.</p></td>
</tr>
<tr class="odd">
<td><p>WINNT_40</p></td>
<td><p>GPD preprocessors for Windows XP, Windows 2000, and Windows NT 4.0</p></td>
<td><p>Environment is Windows NT 4.0.</p></td>
</tr>
<tr class="even">
<td><p>PARSER_VER_1.0</p></td>
<td><p>GPD preprocessors for Windows NT 4.0, Windows 2000, and Windows XP</p></td>
<td><p>GPD parser version 1.0</p></td>
</tr>
</tbody>
</table>

 

The WINNT\_40, WINNT\_50, and WINNT\_51 symbols are useful for creating GPD files that are compatible with Windows NT 4.0, Windows 2000, and Windows XP. If, for example, Windows XP supports a printer capability that is not supported by Windows 2000, then that capability can be specified within a GPD file section that is bounded by \***Ifdef**: WINNT\_51 and \***Endif** directives.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bprint\print%5D:%20Preprocessor%20Directives%20%20RELEASE:%20%289/1/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")

