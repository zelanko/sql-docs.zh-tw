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
manager: jroth
ms.openlocfilehash: ce22c31c4924c050baff2f7d96c224a8c5c3403b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699362"
---
# <a name="required-client-settings"></a>必要用戶端設定
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 指定下列設定，以使用自訂**DataFactory**處理常式。  
  
-   指定 「 提供者 = MS 遠端 」 中[連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)物件[提供者屬性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)屬性或**連接**物件的連接字串 」**提供者**="關鍵字。  
  
-   設定[CursorLocation 屬性 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設**adUseClient**。  
  
-   指定要用於處理常式的名稱[DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的**處理常式**屬性，或有[資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)物件的連接字串 」**處理常式**="關鍵字。 (您無法在中設定處理常式**連線**物件連接字串。)  
  
 RDS 提供名為伺服器上的預設處理常式**MSDFMAP。處理常式**。 （預設值的自訂檔案會命名為 MSDFMAP。INI。)  
  
 **範例**  
  
 假設下列各節中**MSDFMAP。INI**和資料來源名稱、 AdvWorks，先前已定義：  
  
```console
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 在 Visual Basic 中寫入下列程式碼片段：  
  
## <a name="rdsdatacontrol-version"></a>RDS。DataControl 版本  
  
```vb
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "https://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>資料錄集版本  
  
```vb
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 指定[處理常式屬性 (RDS)](../../../ado/reference/rds-api/handler-property-rds.md)屬性或關鍵字;[提供者屬性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)屬性或關鍵字，而*CustomerById*並*CustomerDatabase*識別項。 然後開啟**資料錄集**物件  
  
 rs.Open "CustomerById(4)", "Handler=MSDFMAP.Handler;" & _  
  
```vb
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=https://yourServer"  
```  
  
## <a name="see-also"></a>另請參閱  
 [自訂檔案 Connect 區段](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案 SQL 區段](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自訂檔案 UserList 區段](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自訂檔案](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

