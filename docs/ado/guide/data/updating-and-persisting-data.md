---
title: "更新和保存資料 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e9220fd7448c5c2b7ba9e2600ca129f61e917723
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="updating-and-persisting-data"></a>更新和保存資料
如何使用 ADO 來取得資料來源中的資料、 如何在資料中四處移動以及如何甚至編輯資料，將有討論前述章節。 當然，如果您的應用程式的目標是允許使用者變更資料，您必須了解如何儲存這些變更。 您可能可以保存**資料錄集**變更為檔案，使用**儲存**方法，或者您可以將變更送回儲存體使用的資料來源**更新**或**UpdateBatch**方法。  
  
 在前述章節中，您在變更資料的數個資料列**資料錄集**。 ADO 支援加入、 刪除和修改的資料列與相關的兩個基本概念。  
  
 第一個概念是，不立即變更**資料錄集**; 相反地，它們會對內部*複製緩衝區*。 如果您決定不想變更，則會捨棄複製緩衝區中的修改。 如果您決定要保留變更，複製緩衝區中的變更會套用到**資料錄集**。  
  
 第二個概念是，變更或是傳播到資料來源為您宣告工作的資料列上完成 (亦即*立即*模式)，或直到宣告集的工作，會收集一組資料列的所有變更完成 (亦即*批次*模式)。 **LockType**屬性會決定在變更基礎資料來源。 **Adlockreadonly**或**Locktype**指定即時模式，雖然**Adlockpessimistic**指定批次模式。 **CursorLocation**屬性可能會影響其**LockType**設定都是。 比方說， **Locktype**如果，則不支援設定**CursorLocation**屬性設定為**adUseClient**。  
  
 在即時模式中，每次叫用**更新**方法將變更傳播到資料來源。 在批次模式中，每次叫用**更新**複製緩衝區，但僅限於目前的資料列位置的移動儲存的變更或**UpdateBatch**方法將變更傳播到資料來源。  
  
 此章節包含下列主題。  
  
-   [更新資料](../../../ado/guide/data/updating-data.md)  
  
-   [保存資料](../../../ado/guide/data/persisting-data.md)
