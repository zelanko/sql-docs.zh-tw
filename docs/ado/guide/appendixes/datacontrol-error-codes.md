---
title: "DataControl 錯誤碼 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors [ADO], DataControl
- DataControl errors [ADO]
ms.assetid: 293df9d5-e1a2-406d-9107-07bf7cdc6f96
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 54dcd3721781ccb2889d88c2545d8bb3630cb7bc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="datacontrol-object-error-codes"></a>DataControl 物件錯誤代碼
下表列出[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件錯誤代碼。 正數低的兩個位元組十進位轉譯，就會顯示完整的錯誤程式碼和十六進位值負的十進位轉譯。

|RDSDataControl 錯誤碼|Number|Description|
|---------------------------------|------------|-----------------|
|**IDS_AsyncPending**|4107-2146824175 0x800A1011|暫止非同步作業時，無法執行作業。|
|**IDS_BadInlineTablegram**|4105-2146824183 0x800A1009|不正確的內嵌 tablegram。|
|**IDS_CantConnect**|4099-2146824189 0x800A1003|無法連線到伺服器。|
|**IDS_CantCreateObject**|4100-2146824188 0x800A1004|無法建立商務物件。|
|**IDS_CantFindDataspace**|4102-2146824186 0x800A1006|Dataspace 屬性不是有效的。|
|**IDS_CantInvokeMethod**|4101-2146824187 0x800A1005|無法在商務物件上叫用方法。|
|**IDS_CrossDomainWarning**|4112-2146824170 0x800A1016|此頁面會存取另一個網域上的資料。 若要允許此嗎？ 若要避免此訊息在 Internet Explorer 中的，您可以加入安全的網站信任的網站區域上**安全性** 索引標籤**網際網路選項** 對話方塊。|
|**IDS_InvalidADCClientVersion**|4106-2146824176 0x800A1010|RDS 用戶端版本無效，用戶端是比伺服器。|
|**IDS_INVALIDARG**|5376-2147019520 0x80071500|一或多個引數均為無效。|
|**IDS_InvalidBindings**|4097-2146824191 0x800A1001|繫結屬性中的錯誤。|
|**IDS_InvalidParam**|4110-2146824172 0x800A1014|一或多個引數均為無效。|
|**IDS_NOINTERFACE**|5377-2147019519 0x80071501|支援這類的介面。|
|**IDS_NotReentrant**|4111-2146824171 0x800A1015|事件處理常式仍在處理時，無法執行要求。|
|**IDS_ObjectNotSafe**|4103-2146824185 0x800A1007|在此電腦上的安全設定禁止建立商務物件。|
|**IDS_RecordsetNotOpen**|4109-2146824173 0x800A1013|**資料錄集**未開啟。|
|**IDS_ResetInvalidField**|4108-2146824174 0x800A1012|資料行中指定**SortColumn**或**FilterColumn**不存在。|
|**IDS_RowsetNotUpdateable**|4104-2146824184 0x800A1008|資料列集不能更新。|
|**IDS_UnexpectedError**|4351-2146823937 0x800A10FF|未預期的錯誤。|
|**IDS_UpdatesFailed**|4098-2146824190 0x800A1002|無法更新資料庫。|
|**IDS_URLMONNotFound**|4119-2146824169 0x800A1017|DataControl **URL**屬性需要系統檔案 Urlmon.dll，找不到。|

## <a name="see-also"></a>請參閱＜
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)
