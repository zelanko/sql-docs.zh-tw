---
title: ReadyState 屬性 (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ReadyState property [ADO]
ms.assetid: 5be75bc7-1171-4440-a37e-c8cc6b5cd865
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c575683b5ec23c6739a37eae177be004efea0a57
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63255724"
---
# <a name="readystate-property-rds"></a>ReadyState 屬性 (RDS)
表示進度[DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件，它會擷取資料到其[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|目前的查詢仍在執行，並已經提取的任何資料列。 **DataControl**物件的**資料錄集**不是可供使用。|  
|**adcReadyStateInteractive**|一組初始擷取目前查詢的資料列的已儲存在**DataControl**物件的**資料錄集**和可供使用。 仍然會擷取剩餘的資料列。|  
|**adcReadyStateComplete**|已儲存在由目前的查詢所擷取的所有資料列**DataControl**物件的**資料錄集**和可供使用。<br /><br /> 此狀態也會存在，如果作業已中止，因為發生錯誤，或如果**資料錄集**物件未初始化。|  
  
> [!NOTE]
>  這些常數會使用每個用戶端可執行檔必須提供它們的宣告。 您可以剪下並貼上您想要從檔案 Adcvbs.inc，位於 預設的安裝資料夾的 RDS 程式庫的常數宣告。  
  
## <a name="remarks"></a>備註  
 使用[onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md)事件，以監視中的變更**ReadyState**非同步查詢作業期間的屬性。 這是比定期檢查屬性的值更有效率。  
  
 如果非同步作業期間，發生錯誤**ReadyState**屬性變更為**adcReadyStateComplete**，則[狀態](../../../ado/reference/ado-api/state-property-ado.md)屬性變更從**adStateExecuting**要**adStateClosed**，而**資料錄集**物件[值](../../../ado/reference/ado-api/value-property-ado.md)屬性仍會*Nothing*.  
  
## <a name="applies-to"></a>適用於  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ReadyState 屬性範例 (VBScript)](../../../ado/reference/rds-api/readystate-property-example-vbscript.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [ExecuteOptions 屬性 (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


