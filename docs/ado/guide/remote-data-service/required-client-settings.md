---
title: "需要用戶端設定 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ae0e7f5ebf8126168c8d759ca7b5e8c17864fb26
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="required-client-settings"></a>必要的用戶端設定
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 指定要使用自訂的下列設定**DataFactory**處理常式。  
  
-   指定 「 提供者 = MS 遠端 」 中[連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)物件[提供者屬性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)屬性或**連接**物件的連接字串 」**提供者**="關鍵字。  
  
-   設定[CursorLocation 屬性 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性**adUseClient**。  
  
-   指定要用於處理常式的名稱[DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的**處理常式**屬性，或[資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)物件的連接字串 」**處理常式**="關鍵字。 (您不能設定處理常式**連接**物件連接字串。)  
  
 RDS 指名的伺服器上提供的預設處理常式**MSDFMAP。處理常式**。 （預設的自訂檔案是命名為 MSDFMAP。INI。)  
  
 **範例**  
  
 下面各節中會假設**MSDFMAP。INI**和資料來源名稱、 Advworks<，先前已定義：  
  
```  
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 下列程式碼片段會在 Visual Basic 中寫入：  
  
## <a name="rdsdatacontrol-version"></a>RDSDataControl 版本  
  
```  
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "http://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>資料錄集版本  
  
```  
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 指定[處理常式屬性 (RDS)](../../../ado/reference/rds-api/handler-property-rds.md)屬性或關鍵字;[提供者屬性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)屬性或關鍵字; 而*CustomerById*和*CustomerDatabase*識別項。 然後開啟**資料錄集**物件  
  
 rs。開啟 「 CustomerById(4) 」，「 處理常式 = MSDFMAP。處理常式; 」 （& s) _  
  
```  
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=http://yourServer"  
```  
  
## <a name="see-also"></a>請參閱  
 [自訂檔案連接 > 一節](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自訂檔案 SQL > 一節](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自訂檔案 UserList > 一節](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要的用戶端設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自訂檔](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [撰寫您自己的自訂處理常式](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)






















