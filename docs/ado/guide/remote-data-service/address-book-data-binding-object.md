---
description: 通訊錄資料繫結物件
title: 通訊錄資料系結物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
author: rothja
ms.author: jroth
ms.openlocfilehash: d6b6bb99ea218268a7ccb988acb2f49fb4898f32
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978439"
---
# <a name="address-book-data-binding-object"></a>通訊錄資料繫結物件
通訊錄的應用程式會使用 [RDS。DataControl](../../reference/rds-api/datacontrol-object-rds.md) 物件，可將 SQL Server 資料庫中的資料系結至視覺物件 (在此案例中，會在應用程式的用戶端 HTML 頁面中) DHTML 資料表。 事件驅動的 VBScript 程式邏輯使用 [RDS。DataControl](../../reference/rds-api/datacontrol-object-rds.md) 至：  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
-   查詢資料庫、將更新傳送至資料庫，然後重新整理資料格。  
  
-   允許使用者移至資料方格中的第一個、下一個、上一個或最後一筆記錄。  
  
 下列程式碼會定義 **RDS。DataControl** 元件：  
  
```vb
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 物件標記會定義 **RDS。** 程式中的 DataControl 元件。 標記包含兩種類型的參數：  
  
-   與泛型物件標記相關聯的。  
  
-   RDS 專用的 **。DataControl** 物件。  
  
## <a name="generic-object-tag-parameters"></a>泛型物件標記參數  
 下表描述與物件標記相關聯的參數。  
  
|參數|描述|  
|---------------|-----------------|  
|***CLASSID***|唯一的128位數位，可識別系統的內嵌物件類型。 此識別碼會保留在本機電腦的系統登錄中。 RDS 類別識別碼的 (**。DataControl** 物件，請參閱 [RDS。DataControl 物件](../../reference/rds-api/datacontrol-object-rds.md)。 ) |  
|***識別碼***|針對用來在程式碼中識別的内嵌物件，定義整個檔的識別碼。|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>Rds。DataControl 標記參數  
 下表描述 RDS 特定的參數 **。DataControl** 物件。 如需 RDS 的完整清單， (**。DataControl** 物件參數，以及執行這些參數的時機，請參閱 [RDS。DataControl 物件](../../reference/rds-api/datacontrol-object-rds.md)。 )   
  
|參數|描述|  
|---------------|-----------------|  
|[伺服器](../../reference/rds-api/server-property-rds.md)|如果您使用的是 HTTP，此值會是前面加上的伺服器電腦名稱稱 `https://` 。|  
|[CONNECT](../../reference/rds-api/connect-property-rds.md)|提供 RDS 的必要連接資訊 **。DataControl** 以連接到 SQL Server。|  
|[SQL](../../reference/rds-api/sql-property.md)|設定或傳回用來捕獲 [記錄集](../../reference/ado-api/recordset-object-ado.md)的查詢字串。|  
  
## <a name="see-also"></a>另請參閱  
 [通訊錄命令按鈕](./address-book-command-buttons.md)