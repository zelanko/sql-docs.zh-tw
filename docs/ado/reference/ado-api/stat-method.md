---
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
ms.openlocfilehash: 6295640a0d9ec0815ebac9086efc3835915e0e0c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759774"
---
# <a name="stat-method"></a>Stat 方法
抓取[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>傳回值  
 **長**數值，指出作業的狀態。  
  
#### <a name="parameters"></a>參數  
 *StatStg*  
 STATSTG 結構，將會填入資料流程的相關資訊。 ADO 資料流程物件所使用的**Stat**方法執行並不會填入結構的所有欄位。  
  
 *StatFlag*  
 指定這個方法不會傳回 STATSTG 結構中的某些成員，因此會儲存記憶體配置作業。 值取自 STATFLAG 列舉。 STATFLAG 列舉有兩個值  
  
|持續性|值|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>備註  
 針對 ADO Stream 物件所實作為的 Stat 方法版本會填入 STATSTG 結構的下欄欄位：  
  
 *pwcsName*  
 包含資料流程名稱的字串（如果有的話），而且未指定 StatFlag 值 STATFLAG_NONAME。  
  
 *cbSize*  
 指定資料流或位元組陣列的大小，以位元組為單位。  
  
 *mtime*  
 指示這個儲存區、資料流或位元組陣列的上一次修改時間。  
  
 *ctime*  
 指示這個儲存區、資料流或位元組陣列的建立時間。  
  
 *atime*  
 指示這個儲存區、資料流或位元組陣列的上一次存取時間。  
  
 如果 StatFlag 參數中指定了 STATFLAG_NONAME，就不會傳回資料流程的名稱。  
  
 如果 StatFlag 參數中未指定 STATFLAG_NONAME，而且目前的資料流程沒有可用的名稱，則會 E_NOTIMPL 此值。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
