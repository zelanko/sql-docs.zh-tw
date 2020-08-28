---
description: 更新和保存資料
title: 更新和保存資料 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
author: rothja
ms.author: jroth
ms.openlocfilehash: 05ca0196ef59df1f67d5f65f3abc52133b81869a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979169"
---
# <a name="updating-and-persisting-data"></a>更新和保存資料
上述章節已討論過如何使用 ADO 來取得資料來源中的資料、如何在資料中四處移動，甚至是如何編輯資料。 當然，如果您的應用程式目標是要讓使用者變更資料，您就必須瞭解如何儲存這些變更。 您可以使用**Save**方法將**記錄集**變更保存到檔案中，也可以使用**Update**或**UpdateBatch**方法將變更傳送回資料來源以進行儲存。  
  
 在上一章中，您已變更 **記錄集**的數個數據列中的資料。 ADO 支援兩種與資料列的新增、刪除和修改相關的基本概念。  
  
 第一個概念是不會立即對 **記錄集**進行變更;相反地，它們會對內部 *複製緩衝區*進行。 如果您決定不想要變更，則會捨棄複製緩衝區中的修改。 如果您決定要保留變更，複製緩衝區中的變更會套用至 **記錄集**。  
  
 第二個概念是，當您在資料列上宣告工作時，變更會立即傳播至資料來源 (也就是 *立即* 模式) ，或收集一組資料列的所有變更，直到您宣告 set complete (（ *批次* 模式) ）的工作為止。 **LockType**屬性會決定何時變更基礎資料來源。 **adLockOptimistic** 或 **adLockPessimistic** 會指定立即模式，而 **adLockBatchOptimistic** 則會指定批次模式。 **CursorLocation**屬性可能會影響可用的**LockType**設定。 例如，如果**CursorLocation**屬性設定為**adUseClient**，則不支援**adLockPessimistic**設定。  
  
 在「立即模式」中， **Update** 方法的每個調用都會將變更傳播至資料來源。 在批次模式中，目前資料列位置的 **Update** 或移動的每個調用都會將變更儲存至複製緩衝區，但是只有 **UpdateBatch** 方法會將變更傳播至資料來源。  
  
 此章節包含下列主題。  
  
-   [更新資料](../../../ado/guide/data/updating-data.md)  
  
-   [保存資料](../../../ado/guide/data/persisting-data.md)
