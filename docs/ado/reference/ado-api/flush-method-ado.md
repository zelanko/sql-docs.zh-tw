---
title: Flush 方法（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c00f3c92d3d2bd3111201d6f1536884e3e9dceb5
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760084"
---
# <a name="flush-method-ado"></a>Flush 方法 (ADO)
將 ADO 緩衝區中剩餘的[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)內容強制寫入與**資料流程**相關聯的基礎物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>備註  
 這個方法可以用來將資料流程緩衝區的內容傳送到基礎物件：例如，以 URL 表示的節點或檔案，也就是**資料流程**物件的來源。 當您想要確保已寫入對**資料流程**內容所做的所有變更時，應該呼叫這個方法。 不過，使用 ADO 時，通常不需要呼叫**Flush**，因為 ADO 會持續在背景中盡可能地排清其緩衝區。 對**資料流程**內容所做的變更會自動進行，而不會快取，直到呼叫**Flush**為止。  
  
 使用[Close](../../../ado/reference/ado-api/close-method-ado.md)方法關閉**資料流程**時，會自動排清**資料流程**的內容;在**關閉**之前，不需要立即明確呼叫**Flush** 。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
