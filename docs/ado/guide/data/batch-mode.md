---
title: "批次模式 |Microsoft 文件"
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
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 92e249a7c2d5b0c01e291f4829d5c4f8c580fb2c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="batch-mode"></a>批次模式
批次模式就是作用中時**LockType**屬性設定為**Adlockpessimistic**和提供者所支援批次更新。 無法使用資料指標位置根據特定鎖定類型的設定。 比方說，封閉式鎖定就無法使用類型時**CursorLocation**設**adUseClient**。 相反地，當游標位置是在伺服器上的提供者無法支援批次的開放式鎖定。 您應該使用批次使用索引鍵集或靜態資料指標更新。  
  
 **UpdateBatch**方法用來傳送**資料錄集**變更保留複製緩衝區中要更新資料來源的伺服器。 在下列區段中，我們將會開啟**資料錄集**在批次模式中，複製緩衝區中，進行變更，然後將變更傳送到資料來源使用的呼叫**UpdateBatch**。  
  
 本節包含下列主題：  
  
-   [將更新傳送： UpdateBatch 方法](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [篩選的更新記錄](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [處理失敗的更新](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [偵測和解決衝突](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [中斷並重新連接的資料錄集](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [更新聯結結果： 唯一資料表](../../../ado/guide/data/updating-joined-results-unique-table.md)
