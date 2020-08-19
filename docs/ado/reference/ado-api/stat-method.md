---
description: Stat 方法
title: Stat 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
author: rothja
ms.author: jroth
ms.openlocfilehash: 5375335fe0964107aed54de71d7e700b0588f209
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441990"
---
# <a name="stat-method"></a>Stat 方法
抓取 [資料流程](../../../ado/reference/ado-api/stream-object-ado.md) 物件的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>傳回值  
 **Long**值，指出作業的狀態。  
  
#### <a name="parameters"></a>參數  
 *StatStg*  
 STATSTG 結構，將會填入資料流程的相關資訊。 ADO 資料流程物件所使用之 **Stat** 方法的執行不會填入結構的所有欄位。  
  
 *StatFlag*  
 指定此方法不會傳回 STATSTG 結構中的某些成員，因此會儲存記憶體配置作業。 值取自 STATFLAG 列舉。 STATFLAG 列舉有兩個值  
  
|常數|值|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>備註  
 針對 ADO 資料流程物件所執行的 Stat 方法版本會填入 STATSTG 結構的下欄欄位：  
  
 *pwcsName*  
 字串，其中包含資料流程的名稱（如果有的話），而且未指定 StatFlag 值 STATFLAG_NONAME。  
  
 *cbSize*  
 指定資料流或位元組陣列的大小，以位元組為單位。  
  
 *mtime*  
 指示這個儲存區、資料流或位元組陣列的上一次修改時間。  
  
 *ctime*  
 指示這個儲存區、資料流或位元組陣列的建立時間。  
  
 *atime*  
 指示這個儲存區、資料流或位元組陣列的上一次存取時間。  
  
 如果在 StatFlag 參數中指定 STATFLAG_NONAME，則不會傳回資料流程的名稱。  
  
 如果未在 StatFlag 參數中指定 STATFLAG_NONAME，且目前的資料流程沒有可用的名稱，將會 E_NOTIMPL 此值。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
