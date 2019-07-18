---
title: DataControl 錯誤碼 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], DataControl
- DataControl errors [ADO]
ms.assetid: 293df9d5-e1a2-406d-9107-07bf7cdc6f96
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b59f0f98122d37447e2e702304a31c44073bacfa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926848"
---
# <a name="datacontrol-object-error-codes"></a>DataControl 物件錯誤代碼
下表列出[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件錯誤代碼。 低的兩個位元組的十進位正轉譯，會顯示完整的錯誤程式碼和十六進位值的負值的十進位轉譯。

|RDS。DataControl 錯誤碼|Number|描述|
|---------------------------------|------------|-----------------|
|**IDS_AsyncPending**|4107 -2146824175 0x800A1011|暫止非同步作業時，無法執行作業。|
|**IDS_BadInlineTablegram**|4105 -2146824183 0x800A1009|不正確的內嵌 tablegram。|
|**IDS_CantConnect**|4099 -2146824189 0x800A1003|無法連線到伺服器。|
|**IDS_CantCreateObject**|4100 -2146824188 0x800A1004|無法建立商務物件。|
|**IDS_CantFindDataspace**|4102 -2146824186 0x800A1006|資料空間屬性無效。|
|**IDS_CantInvokeMethod**|4101 -2146824187 0x800A1005|無法在商務物件上叫用方法。|
|**IDS_CrossDomainWarning**|4112 -2146824170 0x800A1016|此頁面會存取另一個網域上的資料。 若要允許此嗎？ 若要避免這個訊息在 Internet Explorer 中的，您可以加入安全的網站信任的網站區域上**安全性**索引標籤**網際網路選項** 對話方塊。|
|**IDS_InvalidADCClientVersion**|4106 -2146824176 0x800A1010|無效的 RDS 用戶端版本的用戶端是比伺服器更新。|
|**IDS_INVALIDARG**|5376 -2147019520 0x80071500|一或多個引數均為無效。|
|**IDS_InvalidBindings**|4097 -2146824191 0x800A1001|繫結屬性中的錯誤。|
|**IDS_InvalidParam**|4110 -2146824172 0x800A1014|一或多個引數均為無效。|
|**IDS_NOINTERFACE**|5377 -2147019519 0x80071501|支援這類的介面。|
|**IDS_NotReentrant**|4111 -2146824171 0x800A1015|無法執行要求，但仍在處理事件處理常式。|
|**IDS_ObjectNotSafe**|4103 -2146824185 0x800A1007|在此電腦上的安全設定禁止建立商務物件。|
|**IDS_RecordsetNotOpen**|4109 -2146824173 0x800A1013|**資料錄集**未開啟。|
|**IDS_ResetInvalidField**|4108 -2146824174 0x800A1012|中指定的資料行**SortColumn**或是**FilterColumn**不存在。|
|**IDS_RowsetNotUpdateable**|4104 -2146824184 0x800A1008|資料列集不能更新。|
|**IDS_UnexpectedError**|4351 -2146823937 0x800A10FF|未預期的錯誤。|
|**IDS_UpdatesFailed**|4098 -2146824190 0x800A1002|無法更新資料庫。|
|**IDS_URLMONNotFound**|4119 -2146824169 0x800A1017|DataControl **URL**屬性需要系統檔案 Urlmon.dll，找不到。|

## <a name="see-also"></a>另請參閱
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)
