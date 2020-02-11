---
title: 跳到記錄 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924938"
---
# <a name="jumping-to-a-record"></a>跳至記錄
[Move](../../../ado/reference/ado-api/move-method-ado.md)方法可讓您使用下列語法，在**記錄集中**向前或向後移動指定的記錄數目：  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>備註  
 所有**記錄集**物件都支援**Move**方法。  
  
 如果*NumRecords*引數大於零，則目前的記錄位置會向前移動（朝**記錄集**的結尾）。 如果*NumRecords*小於零，則目前的記錄位置會向後移動（朝**記錄集**的開頭）。  
  
 如果**移動**呼叫會將目前的記錄位置移至第一筆記錄之前的某個點，ADO 會將目前的記錄設定為**記錄集**內第一筆記錄之前的位置（**BOF**為**True**）。 當**BOF**屬性已經**為 True**時，嘗試向後移動會產生錯誤。  
  
 如果**移動**呼叫會將目前的記錄位置移至最後一筆記錄之後的某個點，ADO 會將目前的記錄設定為**記錄集**內最後一筆記錄之後的位置（**EOF**為**True**）。 當**EOF**屬性已經是**True**時，嘗試繼續進行，會產生錯誤。  
  
 從空的**記錄集**物件呼叫**Move**方法會產生錯誤。  
  
 如果您在*Start*引數中傳遞書簽，則移動會相對於含有此書簽的記錄，假設**記錄集**物件支援書簽。 書簽是使用 [[書簽](../../../ado/reference/ado-api/bookmark-property-ado.md)] 屬性取得。 如果未指定，則移動會相對於目前的記錄。  
  
 如果您使用**CacheSize**屬性從提供者本機快取記錄，傳遞*NumRecords*引數，將目前的記錄位置移到目前的快取記錄群組之外，會強制 ADO 從目的地記錄開始，抓取新的記錄群組。 **CacheSize**屬性會決定新取出群組的大小，而目的地記錄則是第一個抓取的記錄。
