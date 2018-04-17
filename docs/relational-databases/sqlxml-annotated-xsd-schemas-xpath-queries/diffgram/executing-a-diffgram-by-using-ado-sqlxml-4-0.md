---
title: 使用 ADO (SQLXML 4.0) 執行 DiffGram |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], SQLOLEDB Provider
- ADO [SQLXML]
- SQLXMLOLEDB Provider, DiffGrams
- data providers [SQLXML], SQLOLEDB Provider
- DiffGrams [SQLXML], ADO
ms.assetid: 741fce82-de83-4923-86eb-30acb5b9a5e6
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2f53df81d273ec9fa9faecd3dc3dae6ced327775
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="executing-a-diffgram-by-using-ado-sqlxml-40"></a>使用 ADO 執行 DiffGram (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  這個 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 應用程式會使用 ADO 來建立 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的連接，然後執行 DiffGram。 在此應用程式中，DiffGram 和 XSD 結構描述會儲存在一個檔案中。 應用程式會從指定的檔案載入 DiffGram。 您可以使用任何 DiffGrams （及相關聯的 XSD 結構描述） 中所述[DiffGram 範例](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。  
  
 這是範例應用程式的程序：  
  
-   **Conn**物件 (**ADODB。連接**) 建立與特定伺服器上執行的 SQL Server 執行個體的連接。  
  
-   **Cmd**物件 (**ADODB.Command**) 建立的連接上執行。  
  
-   命令用語會設定為 DBGUID_MSSQLXML。  
  
-   DiffGram 會複製到命令資料流 (**strmIn**) 檔案。  
  
-   命令的輸出資料流設**StrmOut**物件 (**ADODB。資料流**) 才能接受任何傳回的資料。  
  
-   當您使用 SQLOLEDB 提供者時，根據預設，您會取得 Sqlxmlx.dll 提供的 Microsoft SQLXML 功能。 若要搭配 SQLOLEDB 提供者使用 Sqlxml4.dll **SQLXML Version**屬性必須設定為**SQLXML.4.0** SQLOLEDB 提供者上**連接**物件。  
  
-   執行命令 (DiffGram)。  
  
 下列程式碼是範例應用程式。  
  
> [!NOTE]  
>  在程式碼中，您必須於連接字串內提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
```  
Private Sub Command1_Click()  
  Dim cmd As New ADODB.Command  
  Dim conn As New ADODB.Connection  
  Dim strmOut As New ADODB.Stream  
  Dim strmIn As New ADODB.Stream  
  
  'Open a connection to SQL Server.  
  conn.Provider = "SQLOLEDB"  
  conn.Open "server=SqlServerName; database=tempdb; Integrated Security=SSPI; "  
  conn.Properties("SQLXML Version") = "SQLXML.4.0"  
  Set cmd.ActiveConnection = conn  
  strmIn.Open  
  strmIn.Charset = "UTF-8"  
  strmIn.LoadFromFile "C:\SomeFilePath\SampleDiffGram.xml"  
  strmIn.Position = 0  
  Set cmd.CommandStream = strmIn  
  
  strmOut.Open  
  cmd.Properties("Output Stream").Value = strmOut  
  cmd.Properties("Output Encoding").Value = "UTF-8"  
  
  cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  cmd.Properties("Mapping Schema") = "C:\SomeFilePath\SampleDiffGram.xml"  
  cmd.Execute , , adExecuteStream  
  strmOut.Position = 0  
  Set cmd = Nothing  
  strmOut.Charset = "UTF-8"  
  strmOut.SaveToFile "C:\DropIt.txt", adSaveCreateOverWrite  
  strmOut.Close  
  Set strmOut = Nothing  
  
End Sub  
```  
  
### <a name="to-test-the-diffgram"></a>若要測試 DiffGram  
  
1.  您的電腦上的資料夾，複製任何一個 DiffGrams 和對應的 XSD 結構描述中的範例之一[DiffGram 範例](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)。  
  
2.  開啟 Visual Basic，然後建立一個標準的 EXE 專案。  
  
3.  將這些參考加入到專案中：  
  
    ```  
    Microsoft ActiveX Data Objects 2.8 Library  
    ```  
  
4.  在工具箱中，按一下  **CommandButton**，然後在表單上繪製一個按鈕。  
  
5.  按兩下該按鈕來編輯程式碼，然後加入主題中提供之應用程式的程式碼。  
  
6.  編輯程式碼以指定 DiffGram 和 XSD 檔案名稱。 同時在適當時，編輯連接字串。  
  
7.  執行應用程式。 執行的結果取決於您所執行的 DiffGram。  
  
  
