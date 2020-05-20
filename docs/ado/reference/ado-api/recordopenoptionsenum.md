---
title: RecordOpenOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
author: rothja
ms.author: jroth
ms.openlocfilehash: 4d97a8cdf2f77f323f0897d7977a2c6945b46b87
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761896"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
指定用於開啟[記錄](../../../ado/reference/ado-api/record-object-ado.md)的選項。 這些值可能會使用或結合。  
  
|持續性|值|說明|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|向提供者指出與**記錄**相關聯的欄位不需要一開始就取得，但可在第一次嘗試存取欄位時抓取。 預設行為（由不存在此旗標表示）是抓取所有**記錄**物件欄位。|  
|**adDelayFetchStream**|0x4000|向提供者指出與**記錄**相關聯的預設資料流程一開始不需要抓取。 預設行為（由不存在此旗標表示）是抓取與**Record**物件相關聯的預設資料流程。|  
|**adOpenAsync**|0x1000|表示以非同步模式開啟**記錄**物件。|  
|**adOpenExecuteCommand**|0x10000|表示來源字串包含應執行的命令文字。 這個值相當於記錄集上的**adCmdText**選項 **。開啟**。|  
|**adOpenRecordUnspecified**|-1|預設值。 指出未指定任何選項。|  
|**adOpenOutput**|0x800000|指出來源是否指向包含可執行腳本的節點（例如）。[ASP] 頁面），則開啟的**記錄**將包含已執行之腳本的結果。 這個值只適用于非集合記錄。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 這些常數沒有 ADO/WFC 對應項。  
  
## <a name="applies-to"></a>套用至  
 [Open 方法 (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)
