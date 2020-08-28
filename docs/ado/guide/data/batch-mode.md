---
description: 批次模式
title: 批次模式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
author: rothja
ms.author: jroth
ms.openlocfilehash: a2cda3a14dc51532d52184f8b2101981d4f36cd3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991599"
---
# <a name="batch-mode"></a>批次模式
當 **LockType** 屬性設定為 **adLockBatchOptimistic** ，而且提供者支援批次更新時，批次模式便會生效。 某些鎖定類型設定無法使用，視資料指標位置而定。 例如，當 **CursorLocation** 設定為 **adUseClient**時，無法使用封閉式鎖定類型。 相反地，當資料指標位置是在伺服器上時，提供者無法支援批次開放式鎖定。 您應該只使用索引鍵集或靜態資料指標來進行批次更新。  
  
 **UpdateBatch**方法是用來將複製緩衝區中保留的**記錄集**變更傳送到伺服器，以更新資料來源。 在下一節中，我們會以批次模式開啟 **記錄集** 、對複製緩衝區進行變更，然後將變更傳送到資料來源，其方式是使用 **UpdateBatch**的呼叫。  
  
 本節包含下列主題：  
  
-   [傳送更新：UpdateBatch 方法](./sending-the-updates-updatebatch-method.md)  
  
-   [篩選更新的記錄](./filtering-for-updated-records.md)  
  
-   [處理失敗的更新](./dealing-with-failed-updates.md)  
  
-   [偵測並解決衝突](./detecting-and-resolving-conflicts.md)  
  
-   [中斷並重新連線資料錄集](./disconnecting-and-reconnecting-the-recordset.md)  
  
-   [更新聯結的結果：唯一資料表](./updating-joined-results-unique-table.md)