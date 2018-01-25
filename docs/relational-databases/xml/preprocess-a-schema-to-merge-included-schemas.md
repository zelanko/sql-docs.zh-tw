---
title: "前置處理結構描述以合併包含的結構描述 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- testing preprocessor tool
- xsd:include
- XML schema collections [SQL Server], preprocessor tool
- include element
- XML schemas [SQL Server], preprocessing
- schema collections [SQL Server], preprocessor tool
- preprocessor tool [XML schemas]
- XML schemas [SQL Server]
ms.assetid: cde1de5f-077a-4a6d-8a81-1ecb6e10d549
caps.latest.revision: "27"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: de002920f313d9a8ce61c1eccde0e02b67468510
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="preprocess-a-schema-to-merge-included-schemas"></a>前置處理結構描述以合併包含的結構描述
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] W3C XSD **include** 項目提供結構描述模組化的支援，在模組化中可以將 XML 結構描述分割成一個以上的實體檔案。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目前不支援這個元素。 伺服器將會拒絕包含此元素的 XML 結構描述。  
  
 可預先處理作為解決方案且包含 \<xsd:include> 指示詞的 XML 結構描述，以便將任何包含結構描述的內容複製和合併成單一結構描述，以利上傳至伺服器。 下列 C#  程式碼可用以預先處理。 在程式碼開始部份的註解提供如何使用它的資訊。  
  
```  
// XSD Schema Include Normalizer  
// To compile:   
// csc filename.cs  
//  
// How to use:  
//  
// Arguments: [-q] input.xsd [output.xsd]  
//  
// input.xsd       - file to normalize  
// output.xsd      - file to output, default is console  
// -q              - quiet  
//   
// Example:  
//   
// filename.exe schema.xsd  
//   
using System;  
using System.Xml;  
using System.Xml.Schema;  
using System.IO;  
using System.Collections;  
public class XsdSchemaNormalizer  
{  
    private static bool NormalizeXmlSchema( String url, TextWriter writer )  
    {  
   try {  
       XmlTextReader txtRead = new XmlTextReader( url );  
       XmlSchema sch = XmlSchema.Read( txtRead, null );  
  
       // Compiling Schema  
       sch.Compile(null);  
  
       XmlSchema outSch =   
      XmlSchemaIncludeNormalizer.BuildIncludeFreeXmlSchema( sch);  
  
       outSch.Write( writer );  
   } catch ( Exception e ) {  
       Console.WriteLine(e.ToString());  
       return false;  
   }  
   return true;  
    }  
    public static void usage()  
    {  
   Console.WriteLine("Arguments: [-q] [-v] input.xsd [output.xsd]\n");  
   Console.WriteLine("input.xsd       - file to normalize");  
   Console.WriteLine("output.xsd      - file to output, default is console");  
   Console.WriteLine("-q              - quiet");  
    }  
    public static void Main(String []args)  
    {  
   if( args.GetLength(0) < 1 ) {  
       usage();  
       return;  
   }  
   int argi = 0;  
   bool quiet = false;  
   if( args[argi] == "-q" ) {  
       quiet = true;  
            argi++;  
   }  
  
   if( argi == args.GetLength(0) )  
   {  
       usage();  
       return;  
   }  
  
   String url = args[argi];  
  
   if( !quiet )  
       Console.WriteLine("Loading Schema: " + url);  
  
   if( argi < ( args.GetLength(0) - 1 ) )  
   {  
       if( !quiet )  
      Console.WriteLine("Outputing to file: " + args[argi+1]);  
  
       StreamWriter output =   
      new StreamWriter( new FileStream(args[argi+1], FileMode.Create ));  
  
       NormalizeXmlSchema( url, output);  
   }  
   else   
   {  
       NormalizeXmlSchema( url, Console.Out);  
   }  
  
    }  
}  
  
// A class to remove all <include> from a Xml Schema  
//  
public class XmlSchemaIncludeNormalizer  
{  
    // Takes as input a XmlSchema which has includes in it   
    // and the schema location uri of that XmlSchema  
    //   
    // Returns a "preprocessed" form of XmlSchema without any   
    // includes. It still retains imports though. Also, it does  
    // not propagate unhandled attributes  
    //  
    // It can throw any exception  
    public static XmlSchema BuildIncludeFreeXmlSchema( XmlSchema inSch )  
    {  
   XmlSchema outSch = new XmlSchema();  
  
   AddSchema( outSch, inSch );  
  
   return outSch;  
    }  
  
    // Adds everything in the second schema minus includes to   
    // the first schema  
    //  
    private static void AddSchema( XmlSchema outSch, XmlSchema add)  
    {  
   outSch.AttributeFormDefault = add.AttributeFormDefault;  
   outSch.BlockDefault = add.BlockDefault;  
   outSch.ElementFormDefault = add.ElementFormDefault;  
   outSch.FinalDefault = add.FinalDefault;  
   outSch.Id = add.Id;  
   outSch.TargetNamespace = add.TargetNamespace;  
   outSch.Version = add.Version;  
  
   AddTableToSchema( outSch, add.AttributeGroups );  
   AddTableToSchema( outSch, add.Attributes );  
   AddTableToSchema( outSch, add.Elements );  
   AddTableToSchema( outSch, add.Groups );  
   AddTableToSchema( outSch, add.Notations );  
   AddTableToSchema( outSch, add.SchemaTypes );  
  
   // Handle includes as a special case  
   for( int i = 0; i < add.Includes.Count; i++ )  
   {  
       if( ! ( add.Includes[i] is XmlSchemaInclude) )  
      outSch.Includes.Add( add.Includes[i] );  
   }  
    }  
  
    // Adds all items in the XmlSchemaObjectTable to the specified XmlSchema  
    //  
    private static void AddTableToSchema( XmlSchema outSch,   
                 XmlSchemaObjectTable table )  
    {  
   IDictionaryEnumerator e = table.GetEnumerator();  
  
   while( e.MoveNext() )  
   {  
       outSch.Items.Add( (XmlSchemaObject)e.Value );  
   }  
    }  
}  
```  
  
## <a name="testing-the-preprocessor-tool"></a>測試前置處理器工具  
 您可以使用下列 XSD 結構描述測試前置處理器工具：  
  
### <a name="bookscommonxsd"></a>books_common.xsd  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
     xmlns="bookstore-schema"  
     elementFormDefault="qualified" >  
  <xsd:element name="publisher" type="xsd:string"/>  
</xsd:schema>  
```  
  
### <a name="booksxsd"></a>books.xsd  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
     xmlns="bookstore-schema"  
     elementFormDefault="qualified"  
     targetNamespace="bookstore-schema">  
  <xsd:include id="books_common" schemaLocation="books_common.xsd"/>  
  <xsd:element name="bookstore" type="xsd:string" />  
</xsd:schema>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 結構描述集合 &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
