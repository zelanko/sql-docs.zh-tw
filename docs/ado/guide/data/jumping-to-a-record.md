---
title: 跳至記錄 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cead84eed4e7689d6b5df907b6a61ef07ab74e8a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924938"
---
# <a name="jumping-to-a-record"></a>跳至記錄
[移動](../../../ado/reference/ado-api/move-method-ado.md)方法可讓您向前或向後在移動**資料錄集**指定的許多的記錄，使用下列語法：  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>備註  
 **移動**方法都支援所有**資料錄集**物件。  
  
 如果*NumRecords*引數是小於或等於零，目前的記錄位置會向前移動 (接近結尾**資料錄集**)。 如果*NumRecords*小於零，目前的記錄位置會向後移動 (開頭**資料錄集**)。  
  
 如果**移動**呼叫會將目前的記錄位置移至第一筆記錄之前的時間點、 ADO 集的目前記錄中的第一個記錄之前的位置**Recordset** (**BOF**已 **，則為 True**)。 嘗試移動時，為了與舊版**BOF**屬性已 **，則為 True**會產生錯誤。  
  
 如果**移動**呼叫會移至某個點目前的記錄位置在最後一筆記錄之後，ADO 集位置的目前記錄中的最後一個記錄之後**Recordset** (**EOF**已 **，則為 True**)。 嘗試移動時，向前**EOF**屬性已 **，則為 True**會產生錯誤。  
  
 呼叫**移動**方法的空**資料錄集**物件會產生錯誤。  
  
 如果您傳遞中的書籤*開始*引數，是相對於與此書籤，記錄的移動假設**資料錄集**物件支援書籤。 使用取得的書籤[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)屬性。 如果未指定，移動是相對於目前的記錄。  
  
 如果您使用**CacheSize**屬性，以在本機快取記錄提供者，並傳遞*NumRecords*移動目前的記錄位置的快取記錄的目前群組外的引數強制 ADO 來擷取一組新的記錄，從 目的記錄。 **CacheSize**屬性會決定新擷取群組的大小和目的地記錄會擷取第一筆記錄。
