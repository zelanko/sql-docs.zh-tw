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
ms.openlocfilehash: 26fabdc205018b8e94575cfb5bd5e945a8fb28ca
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923728"
---
# <a name="updating-and-persisting-data"></a>更新和保存資料
上述章節討論了如何使用 ADO 來取得資料來源中的資料、如何在資料中四處移動，甚至如何編輯資料。 當然，如果您的應用程式目標是允許使用者變更資料，您就必須瞭解如何儲存這些變更。 您可以使用**Save**方法將**記錄集**變更保存至檔案，也可以使用**Update**或**UpdateBatch**方法將變更傳送回資料來源以進行儲存。  
  
 在先前章節中，您已變更**記錄集**的數個數據列中的資料。 ADO 支援兩個與資料列的加入、刪除和修改相關的基本概念。  
  
 第一種概念是，變更不會立即對**記錄集**進行，相反地，它們是對內部*複製緩衝區*進行。 如果您決定不想要變更，則會捨棄複製緩衝區中的修改。 如果您決定要保留變更，複製緩衝區中的變更會套用到**記錄集**。  
  
 第二個概念是，一旦您在完成資料列的工作（也就是*即時模式）* 時，就會立即將變更傳播至資料來源，或對一組資料列進行所有變更，直到您宣告設定完成（也就是*批次*模式）的工作為止。 **LockType**屬性會決定對基礎資料來源進行變更的時間。 **adLockOptimistic**或**adLockPessimistic**會指定立即模式，而**adLockBatchOptimistic**則指定批次模式。 **CursorLocation**屬性可能會影響哪些**LockType**設定可供使用。 例如，如果**CursorLocation**屬性設定為**adUseClient**，則不支援**adLockPessimistic**設定。  
  
 在立即模式中， **Update**方法的每個調用都會將變更傳播至資料來源。 在批次模式中，目前資料列位置的**更新**或移動的每個調用都會儲存複製緩衝區的變更，但只有**UpdateBatch**方法會將變更傳播至資料來源。  
  
 此章節包含下列主題。  
  
-   [更新資料](../../../ado/guide/data/updating-data.md)  
  
-   [保存資料](../../../ado/guide/data/persisting-data.md)
