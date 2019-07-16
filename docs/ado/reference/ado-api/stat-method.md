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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0538a3afae1e4c0bf4159d8ef6a42872f21ff6ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916875"
---
# <a name="stat-method"></a>Stat 方法
擷取有關的資訊[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>傳回值  
 A**長**值，指出作業的狀態。  
  
#### <a name="parameters"></a>參數  
 *StatStg*  
 STATSTG 結構，將會填入資料流的相關資訊。 實作**Stat** ADO Stream 物件所使用的方法不填入所有欄位的結構。  
  
 *StatFlag*  
 指定這個方法不會傳回的某些成員在 STATSTG 結構中，因此節省記憶體配置作業。 值取自 STATFLAG 列舉型別。 STATFLAG 列舉有兩個值  
  
|常數|值|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>備註  
 Stat ADO Stream 物件實作的方法之版本的填滿 STATSTG 結構的下列欄位：  
  
 *pwcsName*  
 未指定包含的資料流，如果有的話和 StatFlag 值 STATFLAG_NONAME 名稱的字串。  
  
 *cbSize*  
 指定的大小，以位元組為單位的資料流或位元組陣列。  
  
 *mtime*  
 表示上次修改時間為這個儲存體、 資料流或位元組陣列。  
  
 *ctime*  
 指示這個儲存體、 資料流或位元組陣列的建立時間。  
  
 *atime*  
 指示這個儲存體、 資料流或位元組陣列上次存取時間。  
  
 如果 STATFLAG_NONAME StatFlag 參數中指定，將不會傳回資料流的名稱。  
  
 如果 STATFLAG_NONAME StatFlag 參數未指定，而且沒有可供目前的資料流的名稱，這個值會是 E_NOTIMPL。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
