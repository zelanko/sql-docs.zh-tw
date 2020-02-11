---
title: DataFactory 物件（RDSServer） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97597e15bc5cd8ee8d3008c97f3a4e8b07b2d43d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964329"
---
# <a name="datafactory-object-rdsserver"></a>DataFactory 物件 (RDSServer)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 這個預設的伺服器端商務物件會執行方法，針對用戶端應用程式提供對指定資料來源的讀取/寫入資料存取。  
  
 **RDSServer. DataFactory**物件的設計是伺服器端自動化物件，它會接收用戶端要求。 在網際網路的執行中，它位於 Web 服務器上，並由 ADISAPI 元件具現化。 **RDSServer. DataFactory**物件提供對指定資料來源的讀取和寫入權限，但不包含任何驗證或商務規則邏輯。  
  
 如果您使用**RDSServer. DataFactory**和 RDS 中提供的方法[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件，遠端資料服務會使用**RDS。預設 DataControl**版本。 預設會假設有一個基本的程式設計案例，也就是**RDSServer. DataFactory**做為一般伺服器端商務物件。  
  
 如果您想要 Web 應用程式處理工作特定的伺服器端處理，您可以使用自訂的商務物件來取代**RDSServer. DataFactory** 。  
  
 您可以建立伺服器端商務物件，以呼叫**RDSServer. DataFactory**方法，例如[Query](../../../ado/reference/rds-api/query-method-rds.md)和[CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)。 如果您想要在商務物件中加入功能，但利用現有的遠端資料服務技術，這會很有説明。  
  
 針對在用戶端上執行的腳本， **DataFactory**物件是不安全的。  
  
 **RDSServer. DataFactory**物件的類別識別碼是9381D8F5-0288-11D0-9501-00AA00B911A5。  
  
 本章節包含下列主題。  
  
-   [DataFactory 物件 (RDSServer) 屬性、方法和事件](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 物件、Query 方法和 CreateObject 方法範例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


