---
title: "什麼是鎖定？ | Microsoft Docs"
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
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 133cd38feed1b55557112abe45872d333cc08c2a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="what-is-a-lock"></a>什麼是鎖定？
鎖定是 DBMS 會存取限制在多使用者環境中的資料列的程序。 資料列或資料行以獨佔方式鎖定時，不允許其他使用者存取鎖定的資料，直到釋放鎖定為止。 這可確保兩位使用者無法同時更新相同的資料行的資料列中。  
  
 鎖定可能會耗費資源的觀點和應該用只在需要時來保留資料完整性。 其中數百或數千名的使用者可能會嘗試存取記錄每秒的資料庫中，例如資料庫連線到網際網路，不必要的鎖定可能很快會導致應用程式中的效能變慢。  
  
 您可以控制如何在資料來源和 ADO 資料指標程式庫管理並行藉由選擇適當的鎖定選項。  
  
 設定**LockType**屬性之前開啟**資料錄集**指定開啟它時，應該使用何種類型的鎖定提供者。 讀取屬性的傳回類型的鎖定上開放使用**資料錄集**物件。  
  
 提供者可能不支援所有的鎖定類型。 如果提供者無法支援所要求**LockType**設定，它會取代另一種鎖定。 若要判斷中可用的實際鎖定功能**資料錄集**物件，請使用[支援](../../../ado/reference/ado-api/supports-method.md)方法**adUpdate**和**adUpdateBatch**.  
  
 **Locktype**如果，則不支援設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient。** 如果設定不支援的值，不會產生錯誤。支援的最接近**LockType**將改為使用。  
  
 **LockType**屬性是讀取/寫入時**資料錄集**是關閉的狀態，或唯讀狀態開啟時。  
  
 此章節包含下列主題。  
  
-   [鎖定的類型](../../../ado/guide/data/types-of-locks.md)
