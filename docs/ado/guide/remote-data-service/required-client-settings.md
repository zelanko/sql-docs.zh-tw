---
title: 必要的用戶端設定 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bdb99cb3d792900f48ceb69c25c7ae720c339683
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922297"
---
# <a name="required-client-settings"></a>必要用戶端設定
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 指定下列設定以使用自訂**DataFactory**處理常式。  
  
-   在[Connection 物件（ado）](../../../ado/reference/ado-api/connection-object-ado.md)物件[提供者屬性（ado）](../../../ado/reference/ado-api/provider-property-ado.md)屬性或**連接**物件連接字串 "**Provider**=" 關鍵字中，指定 "provider = MS Remote"。  
  
-   將[CursorLocation 屬性（ADO）](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。  
  
-   指定要在[DataControl 物件（RDS）](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的**處理常式**屬性中使用的處理常式名稱，或是[記錄集物件（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)物件的連接字串 "**handler**=" 關鍵字。 （您無法在**連接**物件連接字串中設定處理常式）。  
  
 RDS 會在伺服器上提供名為 MSDFMAP 的預設處理常式 **。處理常式**。 （預設的自訂檔案命名為 MSDFMAP。INI）。  
  
 **範例**  
  
 假設 MSDFMAP 中的下列各節 **。** 先前已定義 INI 和資料來源名稱 advworks-srv01：  
  
```console
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 下列程式碼片段是以 Visual Basic 撰寫的：  
  
## <a name="rdsdatacontrol-version"></a>句.DataControl 版本  
  
```vb
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "https://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>記錄集版本  
  
```vb
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 請指定[Handler 屬性（RDS）](../../../ado/reference/rds-api/handler-property-rds.md)屬性或關鍵字;[Provider 屬性（ADO）](../../../ado/reference/ado-api/provider-property-ado.md)屬性或關鍵字;和*CustomerById*和*CustomerDatabase*識別碼。 然後開啟**記錄集**物件  
  
 車載.開啟 "CustomerById （4）"，"Handler = MSDFMAP。處理常式; "& _  
  
```vb
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=https://yourServer"  
```  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案連接區段](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案 SQL 區段](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自訂檔案 UserList 區段](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [瞭解自訂檔案](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

