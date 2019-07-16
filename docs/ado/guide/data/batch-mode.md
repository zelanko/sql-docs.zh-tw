---
title: 批次模式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 188a95f985ac1d578bca8c7e10ac4c4054c935c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925959"
---
# <a name="batch-mode"></a>批次模式
批次模式的作用中時**LockType**屬性設定為**Adlockpessimistic**和批次更新的提供者支援。 無法使用資料指標位置根據特定鎖定類型設定。 比方說，封閉式鎖定類型不適用於何時**CursorLocation**設為**adUseClient**。 相反地，提供者無法支援批次的開放式鎖定，當資料指標位置是在伺服器上。 您應該使用批次使用 keyset 或 static 資料指標更新。  
  
 **UpdateBatch**方法用來傳送**資料錄集**變更保存複製緩衝區中要更新的資料來源的伺服器。 在下一節中，我們便會開啟**Recordset**在批次模式中，變更複製緩衝區中，並再將變更傳送至資料來源使用的呼叫**UpdateBatch**。  
  
 本節包含下列主題：  
  
-   [傳送更新：UpdateBatch 方法](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [篩選更新的記錄](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [處理失敗的更新](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [偵測並解決衝突](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [中斷並重新連接資料錄集](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [更新聯結的結果：唯一資料表](../../../ado/guide/data/updating-joined-results-unique-table.md)
