---
title: 地址通訊錄資料繫結物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da63965c867c56572956ca5400a4b9dcc1281abf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63214834"
---
# <a name="address-book-data-binding-object"></a>通訊錄資料繫結物件
通訊錄應用程式使用[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)繫結至資料的 SQL Server 資料庫 （在此情況下，DHTML 資料表） 的視覺物件在應用程式的用戶端 HTML 頁面中的物件。 事件驅動的 VBScript 程式邏輯會使用[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)來：  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
-   查詢資料庫，將更新傳送至資料庫，並重新整理的資料格。  
  
-   在資料格中，可讓使用者移動，第一筆、 下一步上, 一個或最後一筆記錄。  
  
 下列程式碼定義**rds。DataControl**元件：  
  
```vb
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 物件標記會定義**rds。DataControl**程式中的元件。 標記包含兩種類型的參數：  
  
-   這些泛型的物件標記相關聯。  
  
-   與**rds。DataControl**物件。  
  
## <a name="generic-object-tag-parameters"></a>一般物件 Tag 參數  
 下表描述與物件標記相關聯的參數。  
  
|參數|描述|  
|---------------|-----------------|  
|***CLASSID***|唯一 128 位元數字，識別系統的內嵌物件的型別。 這個識別碼會保留在本機電腦的系統登錄中。 (針對類別 Id **rds。DataControl**資訊，請參閱[rds。DataControl 物件](../../../ado/reference/rds-api/datacontrol-object-rds.md)。)|  
|***ID***|定義用來識別程式碼中的內嵌物件的整個文件的識別碼。|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>RDS。DataControl Tag 參數  
 下表描述的特定參數**rds。DataControl**物件。 (如需完整的清單**rds。DataControl**物件的參數，以及實作它們，請參閱[rds。DataControl 物件](../../../ado/reference/rds-api/datacontrol-object-rds.md)。)  
  
|參數|描述|  
|---------------|-----------------|  
|[SERVER](../../../ado/reference/rds-api/server-property-rds.md)|如果您使用 HTTP，值是前面加上的伺服器電腦的名稱`https://`。|  
|[CONNECT](../../../ado/reference/rds-api/connect-property-rds.md)|會提供必要的連接資訊給**rds。DataControl**連接到 SQL Server。|  
|[SQL](../../../ado/reference/rds-api/sql-property.md)|設定或傳回用來擷取查詢字串[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [通訊錄命令按鈕](../../../ado/guide/remote-data-service/address-book-command-buttons.md)


