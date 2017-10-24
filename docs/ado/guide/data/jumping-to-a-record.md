---
title: "跳至記錄 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19a4275d339132db8efd4b09a313b482fc8cb666
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="jumping-to-a-record"></a>跳至資料錄
[移動](../../../ado/reference/ado-api/move-method-ado.md)方法可讓您移往前或往後在**資料錄集**指定的數目的記錄可以使用下列語法：  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>備註  
 **移動**方法適用於所有**資料錄集**物件。  
  
 如果*NumRecords*引數為大於零，目前的記錄位置前移 (的尾端**資料錄集**)。 如果*NumRecords*小於零，會向後移動目前的記錄位置 (開頭**資料錄集**)。  
  
 如果**移動**呼叫會將目前的記錄位置移至第一筆記錄之前的點、 ADO 中的第一個記錄之前的位置設定為目前的記錄**資料錄集**(**BOF**是**True**)。 嘗試移動回溯時**BOF**內容已出現**True**會產生錯誤。  
  
 如果**移動**呼叫會移至某個點目前的記錄位置最後一筆記錄之後，ADO 最後一筆記錄之後的位置設定為目前的記錄**資料錄集**(**EOF**是**True**)。 嘗試移動時，正向**EOF**內容已出現**True**會產生錯誤。  
  
 呼叫**移動**方法從空**資料錄集**物件會產生錯誤。  
  
 如果您要傳入中的書籤*啟動*相對於與此書籤，記錄的引數，移動的假設**資料錄集**物件支援書籤。 書籤透過使用[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)屬性。 如果未指定，移動的過程相對於目前的記錄。  
  
 如果您使用**CacheSize**屬性，以在本機快取提供者，從記錄傳遞*NumRecords*移動目前的記錄位置快取記錄的目前群組外的引數強制 ADO 来擷取的記錄，從目的記錄開始新的群組。 **CacheSize**屬性會決定新擷取群組的大小和目的記錄是第一個擷取的記錄。

