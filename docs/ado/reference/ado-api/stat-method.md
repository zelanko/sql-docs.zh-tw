---
title: Stat 方法 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b900386c1890d54ec61d3bfd2328f3d173c9300
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282017"
---
# <a name="stat-method"></a>Stat 方法
擷取有關的資訊[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>傳回值  
 A**長**值，指出作業的狀態。  
  
#### <a name="parameters"></a>參數  
 *StatStg*  
 系統會利用資料流的相關資訊填入 STATSTG 結構。 實作**Stat** ADO 資料流物件所使用的方法並不填入所有的結構的欄位。  
  
 *StatFlag*  
 指定此方法不會傳回某些成員在 STATSTG 結構中，因此節省記憶體配置作業。 值取自 STATFLAG 列舉型別。 STATFLAG 列舉有兩個值  
  
|常數|ReplTest1|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|@shouldalert|  
  
## <a name="remarks"></a>備註  
 ADO 資料流物件所實作的 Stat 方法的版本會填入 STATSTG 結構的下列欄位：  
  
 *pwcsName*  
 未指定包含的資料流，如果有的話和 StatFlag 值 STATFLAG_NONAME 名稱的字串。  
  
 *cbSize*  
 指定的大小，以位元組為單位的資料流或位元組陣列。  
  
 *mtime*  
 表示此儲存、 資料流或位元組陣列上次修改的時間。  
  
 *ctime*  
 表示此儲存、 資料流或位元組陣列的建立時間。  
  
 *atime*  
 表示此儲存、 資料流或位元組陣列上次存取時間。  
  
 如果 STATFLAG_NONAME StatFlag 參數中指定，將不會傳回的資料流名稱。  
  
 如果未指定 STATFLAG_NONAME StatFlag 參數中沒有適用於目前資料流的名稱，這個值會是 E_NOTIMPL。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
