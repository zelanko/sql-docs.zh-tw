---
title: Flush 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Flush
- _Stream::raw_Flush
helpviewer_keywords:
- Flush method [ADO]
ms.assetid: 938522b4-f836-4c80-8d27-a598a000f0ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f3d9ab76d2f2ed1a6f5dbeaf58be7d2f919acd3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932548"
---
# <a name="flush-method-ado"></a>Flush 方法 (ADO)
強制的內容[Stream](../../../ado/reference/ado-api/stream-object-ado.md)的基礎物件的 ADO 緩衝區中剩餘**Stream**相關聯。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>備註  
 這個方法可用來將資料流緩衝區的內容傳送至基礎物件： 例如，節點或檔案的來源 URL 表示**Stream**物件。 當您想要確保所有變更，應該呼叫這個方法所做的內容**Stream**已寫入。 不過，搭配 ADO 使用它通常不需要呼叫**排清**，ADO 會持續排清其在背景中最大的緩衝區。 變更的內容**Stream**自動執行，不會快取直到**排清**呼叫。  
  
 關閉**Stream**具有[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法會排清的內容**Stream**自動，不是需要明確呼叫**排清**正前方**關閉**。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
