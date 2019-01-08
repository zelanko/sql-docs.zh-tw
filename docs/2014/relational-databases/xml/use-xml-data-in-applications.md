---
title: 在應用程式中使用 XML 資料 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- parameters [XML in SQL Server]
- XML [SQL Server], ADO
- columns [XML in SQL Server], ADO.NET
- ADO [XML in SQL Server]
- columns [XML in SQL Server], SQL Server Native Client
- xml data type [SQL Server], ADO
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- ADO.NET [XML in SQL Server]
- XML [SQL Server], ADO.NET
- columns [XML in SQL Server], ADO
- xml data type [SQL Server], ADO.NET
- XML [SQL Server], SQL Server Native Client
ms.assetid: 5dabf7e0-c6df-451d-a070-4661f84607fd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e9d40c7624cff181d9955dae461e4d0e534dbb02
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53355488"
---
# <a name="use-xml-data-in-applications"></a>在應用程式中使用 XML 資料
  此主描述在您的應用程式中使用 `xml` 資料類型時，可用的選項有哪些。 此主題包括有關下列項目的資訊：  
  
-   使用 ADO 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 處理 `xml` 類型資料行中的 XML  
  
-   使用 ADO.NET 處理 `xml` 類型資料行的 XML  
  
-   使用 ADO.NET 處理參數中的 `xml` 類型  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-ado-and-sql-server-native-client"></a>使用 ADO 和 SQL Server Native Client 處理 xml 類型資料行中的 XML  
 若要使用 MDAC 元件來存取 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中所引進的類型和功能，您必須在 ADO 連接字串中設定 DataTypeCompatibility 初始化屬性。  
  
 例如，以下 Visual Basic Scripting Edition (VBScript) 範例顯示查詢 `Demographics` 範例資料庫 `Sales.Store` 資料表的 `xml` 資料類型資料行 `AdventureWorks2012` 的結果。 此查詢特別會尋找此資料行，其資料列的 `CustomerID` 等於 `3`的例項值。  
  
```  
Const DS = "MyServer"  
Const DB = "AdventureWorks2012"  
  
Set objConn = CreateObject("ADODB.Connection")  
Set objRs = CreateObject("ADODB.Recordset")  
  
CommandText = "SELECT Demographics" & _  
              " FROM Sales.Store" & _  
              " INNER JOIN Sales.Customer" & _  
              " ON Sales.Store.BusinessEntityID = sales.customer.StoreID" & _  
              " WHERE Sales.Customer.CustomerID = 3" & _  
              " OR Sales.Customer.CustomerID = 4"  
  
ConnectionString = "Provider=SQLNCLI11" & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;" & _  
                   "DataTypeCompatibility=80"  
  
'Connect to the data source.  
objConn.Open ConnectionString  
  
'Execute command through the connection and display  
Set objRs = objConn.Execute(CommandText)  
  
Dim rowcount  
rowcount = 0  
Do While Not objRs.EOF  
   rowcount = rowcount + 1  
   MsgBox "Row " & rowcount & _  
           vbCrLf & vbCrLf & objRs(0)  
   objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
```  
  
 此範例顯示如何設定資料類型相容性屬性。 當您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 時，預設會設定為 0。 如果您將此值設定為 80，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 提供者會讓 `xml` 和使用者定義類型的資料行顯示為 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 資料類型。 分別是 DBTYPE_WSTR 和 DBTYPE_BYTES。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您也必須在用戶端電腦上安裝 Native Client，而且連接字串必須以 "`Provider=SQLNCLI11;...`" 指定它當作資料提供者。  
  
#### <a name="to-test-this-example"></a>若要測試此範例  
  
1.  確認已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client，而且用戶端電腦上可以使用 MDAC 2.6.0 或更新版本。  
  
     如需詳細資訊，請參閱 [SQL Server Native Client 程式設計](../native-client/sql-server-native-client-programming.md)。  
  
2.  確認已在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 範例資料庫。  
  
     此範例需要 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫。  
  
3.  複製此主題先前顯示的程式碼，並將程式碼貼到文字編輯器或程式碼編輯器。 將檔案儲存為 HandlingXmlDataType.vbs。  
  
4.  依您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝所需修改指令碼，並儲存變更。  
  
     例如，您應該將 `MyServer` 更改為 `(local)` 或安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之伺服器的實際名稱。  
  
5.  執行 HandlingXmlDataType.vbs，並執行指令碼。  
  
 結果應該類似以下範例輸出：  
  
```  
Row 1  
  
<StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>1500000</AnnualSales>  
  <AnnualRevenue>150000</AnnualRevenue>  
  <BankName>Primary International</BankName>  
  <BusinessType>OS</BusinessType>  
  <YearOpened>1974</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>38000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>40</NumberEmployees>  
</StoreSurvey>  
  
Row 2  
  
<StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>United Security</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1976</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>6000</SquareFeet>  
  <Brands>2</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>5</NumberEmployees>  
</StoreSurvey>  
```  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-adonet"></a>使用 ADO.NET 處理 xml 類型資料行的 XML  
 若要處理來自 XML`xml`使用 ADO.NET 的資料類型資料行和[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]您可以使用的標準行為`SqlCommand`類別。 例如，使用 `xml` 擷取 `SqlDataReader` 資料類型資料行及其值，就跟擷取 SQL 資料行的方式一樣。不過，如果您想要將 `xml` 資料類型的內容處理為 XML，您就必須先將內容指定為 `XmlReader` 類型。  
  
 如需詳細資訊及範例程式碼，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] SDK 文件集的 "XML Column Values in a Data Reader"。  
  
## <a name="handling-an-xml-type-column-in-parameters-by-using-adonet"></a>使用 ADO.NET 處理參數中的 xml 類型資料行  
 若要以 ADO.NET 和 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 處理傳遞為參數的 xml 資料類型，您可以提供值作為 `SqlXml` 資料類型的例項。 這裡不牽涉特殊的處理，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 `xml` 資料類型資料行可以接受與其他資料行及資料類型 (如 `string` 或 `integer`) 相同方式的參數值。  
  
 如需詳細資訊及範例程式碼，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] SDK 文件集的 "XML Values as Command Parameters"。  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料 &#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
