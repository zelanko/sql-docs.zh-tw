---
description: RecordOpenOptionsEnum
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
ms.openlocfilehash: dbddab9f7536c311d55f83fc9c6ea443c3757fa3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442450"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
指定用於開啟 [記錄](../../../ado/reference/ado-api/record-object-ado.md)的選項。 您可以使用或來結合這些值。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|向提供者表示，一開始就不需要抓取與 **記錄** 相關聯的欄位，但在第一次嘗試存取欄位時可以取出這些欄位。 預設行為（以沒有此旗標表示）是要抓取所有 **記錄** 物件欄位。|  
|**adDelayFetchStream**|0x4000|向提供者表示，一開始不需要抓取與 **記錄** 相關聯的預設資料流程。 預設行為（以沒有此旗標表示）是要抓取與 **記錄** 物件相關聯的預設資料流程。|  
|**adOpenAsync**|0x1000|表示以非同步模式開啟 **記錄** 物件。|  
|**adOpenExecuteCommand**|0x10000|指出來源字串包含應該執行的命令文字。 此值相當於記錄集上的 **adCmdText** 選項 **。開啟**。|  
|**adOpenRecordUnspecified**|-1|預設值。 指出未指定任何選項。|  
|**adOpenOutput**|0x800000|指出如果來源指向包含可執行腳本的節點， (例如。ASP 頁面) ，開啟的 **記錄** 將包含所執行腳本的結果。 此值僅適用于非集合記錄。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 這些常數沒有 ADO/WFC 對等專案。  
  
## <a name="applies-to"></a>套用至  
 [Open 方法 (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)
