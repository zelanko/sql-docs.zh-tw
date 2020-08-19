---
description: DataFactory 物件 (RDSServer)
title: DataFactory 物件 (RDSServer) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a27d7911b00e5172941245ef5dcd587345aa1fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439100"
---
# <a name="datafactory-object-rdsserver"></a>DataFactory 物件 (RDSServer)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 這個預設的伺服器端商務物件會針對用戶端應用程式的指定資料來源，執行提供讀取/寫入資料存取的方法。  
  
 **RDSServer. DataFactory**物件是設計為接收用戶端要求的伺服器端自動化物件。 在網際網路的執行中，它位於 Web 服務器上，並由 ADISAPI 元件具現化。 **RDSServer. DataFactory**物件提供對指定資料來源的讀取和寫入存取權，但不包含任何驗證或商務規則邏輯。  
  
 如果您使用 **RDSServer. DataFactory** 和 RDS 提供的方法 [。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 物件，遠端資料服務會使用 **RDS。** 預設為 DataControl 版本。 預設會假設有一個基本的程式設計案例，其中 **RDSServer DataFactory** 做為一般伺服器端商務物件。  
  
 如果您想要讓 Web 應用程式處理工作特定的伺服器端處理，您可以使用自訂商務物件來取代 **RDSServer. DataFactory** 。  
  
 您可以建立會呼叫 **RDSServer. DataFactory** 方法的伺服器端商務物件，例如 [Query](../../../ado/reference/rds-api/query-method-rds.md) 和 [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)。 如果您想要將功能新增至您的商務物件，但利用現有的遠端資料服務技術，這會很有説明。  
  
 **DataFactory**物件對於用戶端上執行的腳本而言並不安全。  
  
 **RDSServer. DataFactory**物件的類別識別碼是9381D8F5-0288-11D0-9501-00AA00B911A5。  
  
 本節包含下列主題。  
  
-   [DataFactory 物件 (RDSServer) 屬性、方法和事件](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 物件、Query 方法和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


