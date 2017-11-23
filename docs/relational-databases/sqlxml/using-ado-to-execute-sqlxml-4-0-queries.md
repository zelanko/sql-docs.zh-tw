---
title: "使用 ADO 執行 SQLXML 4.0 查詢 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- query testers [SQLXML]
- test scripts
- ADO [SQLXML]
- queries [SQLXML], ADO
- SQLXML, ADO
ms.assetid: 3d54e3bb-7c5f-427e-82f8-1403a54c4f53
caps.latest.revision: "23"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0488f2e0e78fc2f915619a6ef0ee7caf6efe5531
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="using-ado-to-execute-sqlxml-40-queries"></a>使用 ADO 執行 SQLXML 4.0 查詢
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]在舊版的 SQLXML 中，被支援 HTTP 為基礎的查詢執行使用 SQLXML IIS 虛擬目錄和 SQLXML ISAPI 篩選器。 在 SQLXML 4.0 中已經移除這些元件，因為自 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始引進的原生 XML Web 服務提供了類似且重疊的功能。  
  
 另一種選擇是利用在 Microsoft Data Access Components (MDAC) 2.6 和更新版本中初次引進的 ActiveX Data Objects (ADO) 的 SQL XML 延伸模組來執行查詢，並使用 SQLXML 4.0 來搭配以 COM 為基礎的應用程式。  
  
 本主題示範如何使用 SQLXML 和 ADO 的 Visual Basic Scripting Edition (VBScript) 應用程式 （具有.vbs 副檔名的指令碼） 的一部分。 本主題提供初始的安裝程序，以協助您重建和測試 SQLXML 4.0 文件集中的查詢範例。  
  
## <a name="creating-the-sqlxml-40-test-script"></a>建立 SQLXML 4.0 測試指令碼  
 在此程序中，您會建立 VBScript (.vbs) 檔案 Sqlxml4test.vbs，這個檔案可利用 ADO 2.6 和更新版本的 SQLXML ADO 延伸模組來執行 SQLXML 查詢。  
  
#### <a name="to-create-the-sqlxml-40-query-tester-using-ado-vbscript"></a>使用 ADO (VBScript) 建立 SQLXML 4.0 查詢測試者  
  
1.  複製以下的程式碼並將其貼入文字檔案。 將檔案儲存為 Sqlxml4test.vbs。  
  
    ```  
    WScript.Echo "Query process may take a few seconds to complete. Please be patient."  
  
    ' Note that for SQL Server Native Client to be used as the data provider,  
    ' it needs to be installed on the client computer first. Also, SQLXML extensions   
    ' for ADO are used and available in MDAC 2.6 or later.  
  
    'Set script variables.  
    inputFile = "@@FILE_NAME@@"  
    strServer = "@@SERVER_NAME@@"  
    strDatabase = "@@DATABASE_NAME@@"  
    dbGuid = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  
    ' Establish ADO connection to SQL Server and   
    ' create an instance of the ADO Command object.  
    Set conn = CreateObject("ADODB.Connection")  
    Set cmd = CreateObject("ADODB.Command")  
    conn.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Server=" & strServer & _  
              ";Database=" & strDatabase & ";Integrated Security=SSPI"  
    Set cmd.ActiveConnection = conn  
  
    ' Create the input stream as an instance of the ADO Stream object.  
    Set inStream = CreateObject("ADODB.Stream")  
    inStream.Open  
    inStream.Charset = "utf-8"  
    inStream.LoadFromFile inputFile  
  
    ' Set ADO Command instance to use input stream.  
    Set cmd.CommandStream = inStream  
  
    ' Set the command dialect.  
    cmd.Dialect = dbGuid  
  
    ' Set a second ADO Stream instance for use as a results stream.   
    Set outStream = CreateObject("ADODB.Stream")  
    outStream.Open  
  
    ' Set dynamic properties used by the SQLXML ADO command instance.   
    cmd.Properties("XML Root").Value = "ROOT"  
    cmd.Properties("Output Encoding").Value = "UTF-8"  
  
    ' Connect the results stream to the command instance and execute the command.  
    cmd.Properties("Output Stream").Value = outStream  
    cmd.Execute , , 1024  
  
    ' Echo cropped/partial results to console.  
    WScript.Echo Left(outStream.ReadText, 1023)  
  
    inStream.Close  
    outStream.Close  
    ```  
  
2.  針對您正嘗試測試的範例及您的測試環境更新下列的指令碼值。  
  
    -   尋找 "`@@FILE_NAME@@`"，並以您的範例檔名稱加以取代。  
  
    -   尋找 "`@@SERVER_NAME@@`"，並以您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱加以取代 (例如，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在本機執行，則為 "`(local)`")。  
  
    -   尋找 "`@@DATABASE_NAME@@`"，並以資料庫的名稱加以取代 (例如，"`AdventureWorks2012`" 或 "`tempdb`")。  
  
     更新任何的其他值 (若您嘗試在電腦本機上重新建立之範例的特定指示中有提及)。  
  
3.  儲存並關閉檔案。  
  
4.  確認您已建立了任何其他的檔案，例如屬於您嘗試在電腦本機上重新建立之範例的 XML 範本或結構描述。 這些檔案應該位於與您儲存測試指令碼檔案 (Sqlxml4test.vbs) 相同的目錄中。  
  
5.  請遵照下一節中的指示來使用 SQLXML 4.0 測試指令碼。  
  
## <a name="using-the-sqlxml-40-test-script"></a>使用 SQLXML 4.0 測試指令碼  
 下列程序描述如何使用 Sqlxml4test.vbs 檔案來測試本文件集所提供的範例查詢。  
  
#### <a name="to-use-the-sqlxml-40-query-tester"></a>使用 SQLXML 4.0 查詢測試者  
  
1.  確認已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client，如下所示：  
  
    1.  從**啟動**功能表上，指向**設定**，然後按一下 **控制台**。  
  
    2.  在控制台中開啟**新增或移除程式**  
  
    3.  在目前安裝的程式清單中，確認**Microsoft SQL Server Native Client**出現在清單中。  
  
        > [!NOTE]  
        >  如果您需要安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端，請參閱[安裝 SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)。  
  
2.  確認用戶端電腦所安裝的 MDAC 版本為 2.6 或更新版本。 如果需要確認 MDAC 版本資訊，可以使用 MDAC Component Checker 工具，此工具可從 Microsoft 網站 (www.microsoft.com) 免費下載。 如需詳細資訊，請在 Microsoft 網站上搜尋 "MDAC Component Checker"。  
  
3.  執行指令碼。  
  
     您可以在命令列使用 Cscript.exe 來執行 VBScript 檔案，或者按兩下 Sqlxml4test.vbs 檔案來叫用 Windows Script Host (WScript.exe)。  
  
     此指令碼在執行時會顯示訊息，警示您指令碼可能需要一些時間執行，才能將查詢結果傳回並顯示為指令碼輸出。 當輸出出現時，請將其內容與範例的預期結果比較。  
  
  
