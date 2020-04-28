---
title: ReadyState 屬性（RDS） |Microsoft Docs
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
ms.openlocfilehash: 8a2a3d22f30a865687e38aedfaf6e688e677efae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963589"
---
# <a name="readystate-property-rds"></a>ReadyState 屬性 (RDS)
指出[DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件將資料抓取到其[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件時的進度。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**adcReadyStateLoaded**|目前的查詢仍在執行中，而且未提取任何資料列。 **DataControl**物件的**記錄集**無法供使用。|  
|**adcReadyStateInteractive**|目前查詢所抓取的初始資料列集已經儲存在**DataControl**物件的**記錄集**內，並可供使用。 剩餘的資料列仍在提取中。|  
|**adcReadyStateComplete**|目前查詢所抓取的所有資料列都已儲存在**DataControl**物件的**記錄集**內，並可供使用。<br /><br /> 如果作業因錯誤而中止，或**記錄集**物件未初始化，則此狀態也會存在。|  
  
> [!NOTE]
>  每個使用這些常數的用戶端可執行檔都必須提供宣告給它們。 您可以從位於 RDS 程式庫的預設安裝資料夾中的 Adcvbs 檔案，剪下並貼上您想要的常數宣告。  
  
## <a name="remarks"></a>備註  
 在非同步查詢作業期間，使用[onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md)事件來監視**ReadyState**屬性中的變更。 這比定期檢查屬性的值更有效率。  
  
 如果在非同步作業期間發生錯誤， **ReadyState**屬性會變更為**adcReadyStateComplete**， [State](../../../ado/reference/ado-api/state-property-ado.md)屬性會從**AdStateExecuting**變更為**adStateClosed**，而且**記錄集**物件[值](../../../ado/reference/ado-api/value-property-ado.md)屬性*會維持不*變。  
  
## <a name="applies-to"></a>套用至  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>另請參閱  
 [ReadyState 屬性範例（VBScript）](../../../ado/reference/rds-api/readystate-property-example-vbscript.md)   
 [Cancel 方法（RDS）](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [ExecuteOptions 屬性 (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


