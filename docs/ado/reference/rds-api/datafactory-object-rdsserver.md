---
title: "DataFactory 物件 (RDSServer) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3df928f2c2ac6735bc1654b1f9eacb02cb202b42
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="datafactory-object-rdsserver"></a>DataFactory 物件 (RDSServer)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 這個預設的伺服器端的商務物件會實作提供到指定的資料來源的用戶端應用程式的讀取/寫入的資料存取的方法。  
  
 **RDSServer.DataFactory**物件的設計是以伺服器端 Automation 物件會接收用戶端要求。 在網際網路實作中，它位於 Web 伺服器，並由 ADISAPI 元件具現化。 **RDSServer.DataFactory**物件所提供的讀取和寫入權限指定的資料來源，但不包含任何驗證或商務規則邏輯。  
  
 如果您使用的方法中都提供**RDSServer.DataFactory**和[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件時，遠端資料服務會使用**.RDSDataControl**預設版本。 預設會假設基本程式設計案例中，其中**RDSServer.DataFactory**做為一般的伺服器端商務物件。  
  
 如果您想 Web 應用程式以處理特定工作的伺服器端處理時，您可以取代**RDSServer.DataFactory**的自訂商務物件。  
  
 您可以建立伺服器端的商務物件的呼叫**RDSServer.DataFactory**方法，例如[查詢](../../../ado/reference/rds-api/query-method-rds.md)和[CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)。 這是有幫助，如果您想要將功能加入至您的商務物件，但利用現有的遠端資料服務技術。  
  
 **DataFactory**物件不是安全的用戶端執行的指令碼。  
  
 類別識別碼**RDSServer.DataFactory**物件是 9381D8F5 0288年 11 D 0 9501 00AA00B911A5。  
  
 本章節包含下列主題。  
  
-   [DataFactory 物件 (RDSServer) 屬性、方法和事件](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>請參閱＜  
 [DataFactory 物件、Query 方法和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


