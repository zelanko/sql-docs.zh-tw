---
title: 更新和保存資料 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d53891b4e82b3ae391d095e8cbca2189fb201d29
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63142957"
---
# <a name="updating-and-persisting-data"></a>更新和保存資料
上述的章節討論如何使用 ADO 以在資料來源取得資料、 如何在資料中四處移動以及如何甚至編輯資料。 當然，如果您的應用程式的目標是允許使用者對資料進行變更，您必須了解如何儲存這些變更。 您可能可以保存**資料錄集**變更為檔案，使用**儲存**方法，或者您可以將變更傳回的資料來源使用儲存體**Update**或**UpdateBatch**方法。  
  
 在前述章節中，您可以變更數個資料列中的資料**資料錄集**。 ADO 支援加入、 刪除和修改的資料列的資料與相關的兩個基本概念。  
  
 第一個概念是，不立即變更**Recordset**; 相反地，它們不會對內部*複製緩衝區*。 如果您決定不想變更，則在複製緩衝區的修改都會被捨棄。 如果您決定要保留變更，複製緩衝區中的變更會套用至**資料錄集**。  
  
 第二個概念是，變更可以傳播到資料來源為您宣告工作的資料列完成 (亦即*立即*模式)，或直到您宣告集的工作，會收集一組資料列的所有變更完成 (亦即*批次*模式)。 **LockType**屬性會決定當基礎資料來源進行變更。 **adLockOptimistic**或是**Locktype**指定即時模式，雖然**Adlockpessimistic**指定批次模式。 **CursorLocation**屬性會影響這**LockType**設定都是。 比方說， **Locktype**如果，則不支援設定**CursorLocation**屬性設定為**adUseClient**。  
  
 在直接模式中，每次叫用**更新**方法將變更傳播到資料來源。 在批次模式中，每次叫用**更新**或目前的資料列位置的移動會將變更儲存至複製的緩衝區，但僅限於**UpdateBatch**方法將變更傳播到資料來源。  
  
 此章節包含下列主題。  
  
-   [更新資料](../../../ado/guide/data/updating-data.md)  
  
-   [保存資料](../../../ado/guide/data/persisting-data.md)
