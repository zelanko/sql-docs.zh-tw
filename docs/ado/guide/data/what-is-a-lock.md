---
description: 什麼是鎖定？
title: 什麼是鎖定？ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
author: rothja
ms.author: jroth
ms.openlocfilehash: d64d6b417f6430cb834c48b8caf93e041a2084e8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978869"
---
# <a name="what-is-a-lock"></a>什麼是鎖定？
鎖定是 DBMS 在多使用者環境中限制存取資料列的進程。 獨佔鎖定資料列或資料行時，不允許其他使用者存取鎖定的資料，直到釋放鎖定為止。 這可確保兩個使用者無法同時更新資料列中的相同資料行。  
  
 從資源的觀點來看，鎖定可能相當昂貴，而且只有在需要保留資料完整性時才應該使用。 在每秒有數百或數千位使用者嘗試存取記錄的資料庫中（例如，連接到網際網路的非必要鎖定的資料庫），可能會在您的應用程式中快速導致效能變慢。  
  
 您可以藉由選擇適當的鎖定選項，來控制資料來源和 ADO 資料指標程式庫管理並行的方式。  
  
 在開啟記錄集之前設定 **LockType** 屬性，以指定提供者在開啟 **記錄集** 時應使用的鎖定類型。 讀取屬性，以傳回在開啟的 **記錄集** 物件上使用的鎖定類型。  
  
 提供者可能不支援所有鎖定類型。 如果提供者無法支援要求的 **LockType** 設定，則會替代另一種類型的鎖定。 若要判斷 **記錄集** 物件中可用的實際鎖定功能，請使用 [支援](../../../ado/reference/ado-api/supports-method.md) 方法搭配 **adUpdate** 和 **adUpdateBatch**。  
  
 如果[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為 adUseClient，則不支援**adLockPessimistic**設定 **。** 如果設定了不支援的值，則不會產生任何錯誤;將改用最接近的支援 **LockType** 。  
  
 當**記錄集**關閉時， **LockType**屬性是讀取/寫入，而當記錄開啟時，則為唯讀屬性。  
  
 此章節包含下列主題。  
  
-   [鎖定的類型](../../../ado/guide/data/types-of-locks.md)
