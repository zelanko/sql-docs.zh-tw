---
description: 必要用戶端設定
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d21cf3f08b284ed2642f9567ae86909fb35579b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452020"
---
# <a name="required-client-settings"></a>必要用戶端設定
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 指定下列設定，以使用自訂 **DataFactory** 處理常式。  
  
-   在連線物件中指定 "Provider = MS Remote"， [ (ado) ](../../../ado/reference/ado-api/connection-object-ado.md) Object [PROVIDER 屬性 (ado) ](../../../ado/reference/ado-api/provider-property-ado.md) 屬性或 **連接** 物件連接字串 "**Provider**=" 關鍵字。  
  
-   將 [ [CursorLocation] 屬性 (ADO) ](../../../ado/reference/ado-api/cursorlocation-property-ado.md) ] 屬性設定為 [ **adUseClient**]。  
  
-   在 DataControl 物件中指定要用於物件的處理常式名稱[ (RDS) ](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的**處理常式**屬性，或 (ADO) 物件的連接字串 "**handler**=" 關鍵字中的[記錄集物件](../../../ado/reference/ado-api/recordset-object-ado.md)。  (您無法在 **連接** 物件連接字串中設定處理常式。 )   
  
 RDS 在名為 MSDFMAP 的伺服器上提供預設處理常式 **。處理常式**。  (預設自訂檔案的名稱為 MSDFMAP.INI。 )   
  
 **範例**  
  
 假設先前已定義 **MSDFMAP.INI** 中的下列區段和資料來源名稱 advworks-srv01：  
  
```console
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 下列程式碼片段會以 Visual Basic 撰寫：  
  
## <a name="rdsdatacontrol-version"></a>Rds。DataControl 版本  
  
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
  
 請指定 (RDS) 屬性或關鍵字的 [處理常式屬性 ](../../../ado/reference/rds-api/handler-property-rds.md) ; [Provider 屬性 (ADO) ](../../../ado/reference/ado-api/provider-property-ado.md) Property 或關鍵字;以及 *CustomerById* 和 *CustomerDatabase* 識別碼。 然後開啟 **記錄集** 物件  
  
 Rs。開啟 "CustomerById (4) "，"Handler = MSDFMAP。處理常式; "& _  
  
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

