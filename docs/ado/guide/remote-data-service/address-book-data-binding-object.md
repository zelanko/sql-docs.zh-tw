---
title: "解決活頁簿的資料繫結物件 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9689d8c41a899c9446f3f21ede83ea88c68b77a3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="address-book-data-binding-object"></a>通訊錄資料繫結物件
通訊錄應用程式會使用[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)繫結至資料的 SQL Server 資料庫 （在這個情況下，DHTML 資料表） 的視覺物件在應用程式的用戶端 HTML 網頁中的物件。 事件驅動的 VBScript 程式邏輯會使用[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)至：  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
-   查詢資料庫、 將更新傳送至資料庫，以及重新整理的資料格。  
  
-   允許使用者移動，第一種，接下來上, 一個或最後一筆記錄，在資料格中。  
  
 下列程式碼定義**.RDSDataControl**元件：  
  
```  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="http://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 OBJECT 標記定義**.RDSDataControl**元件程式中。 標記包含兩種類型的參數：  
  
-   泛型物件標記相關聯。  
  
-   這些特定**.RDSDataControl**物件。  
  
## <a name="generic-object-tag-parameters"></a>泛用物件標記參數  
 下表描述與物件標籤相關聯的參數。  
  
|매개 변수|Description|  
|---------------|-----------------|  
|***CLASSID***|唯一的、 128 位元數字，識別系統的內嵌物件的型別。 這個識別碼是在本機電腦的系統登錄中維護。 (如類別 Id **.RDSDataControl**物件，請參閱[.RDSDataControl 物件](../../../ado/reference/rds-api/datacontrol-object-rds.md)。)|  
|***識別碼***|定義用來識別程式碼中的內嵌物件的整個文件的識別項。|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>RDSDataControl 標記參數  
 下表描述的特定參數**.RDSDataControl**物件。 (如需完整的清單**.RDSDataControl**物件參數，以及何時實作它們，請參閱[.RDSDataControl 物件](../../../ado/reference/rds-api/datacontrol-object-rds.md)。)  
  
|매개 변수|Description|  
|---------------|-----------------|  
|[SERVER](../../../ado/reference/rds-api/server-property-rds.md)|如果您使用 HTTP，值是前面加上的伺服器電腦的名稱`http://`。|  
|[CONNECT](../../../ado/reference/rds-api/connect-property-rds.md)|會提供必要的連接資訊給**.RDSDataControl**連接到 SQL Server。|  
|[SQL](../../../ado/reference/rds-api/sql-property.md)|設定或傳回用來擷取查詢字串[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [通訊錄命令按鈕](../../../ado/guide/remote-data-service/address-book-command-buttons.md)


