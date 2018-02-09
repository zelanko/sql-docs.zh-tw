---
title: "批次模式 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 048fbd6f43bd78612c810049a07788e659a4139d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="batch-mode"></a>批次模式
批次模式就是作用中時**LockType**屬性設定為**Adlockpessimistic**和提供者所支援批次更新。 無法使用資料指標位置根據特定鎖定類型的設定。 比方說，封閉式鎖定就無法使用類型時**CursorLocation**設**adUseClient**。 相反地，當游標位置是在伺服器上的提供者無法支援批次的開放式鎖定。 您應該使用批次使用索引鍵集或靜態資料指標更新。  
  
 **UpdateBatch**方法用來傳送**資料錄集**變更保留複製緩衝區中要更新資料來源的伺服器。 在下列區段中，我們將會開啟**資料錄集**在批次模式中，複製緩衝區中，進行變更，然後將變更傳送到資料來源使用的呼叫**UpdateBatch**。  
  
 本節包含下列主題：  
  
-   [傳送更新：UpdateBatch 方法](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [篩選更新的記錄](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [處理失敗的更新](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [偵測並解決衝突](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [中斷並重新連接資料錄集](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [更新聯結的結果：唯一資料表](../../../ado/guide/data/updating-joined-results-unique-table.md)
