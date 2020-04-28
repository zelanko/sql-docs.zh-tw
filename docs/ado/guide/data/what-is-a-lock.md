---
title: 什麼是鎖定？ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1607c9434e6c30ffd317277aadab27af96868fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923446"
---
# <a name="what-is-a-lock"></a>什麼是鎖定？
鎖定是 DBMS 在多使用者環境中限制資料列存取權的進程。 獨佔鎖定資料列或資料行時，除非釋放鎖定，否則不允許其他使用者存取鎖定的資料。 這可確保兩個使用者無法同時更新資料列中的相同資料行。  
  
 鎖定可能會因為資源的觀點而昂貴，而且只有在需要保留資料完整性時才應該使用。 在有數百或數千名使用者每秒都可能嘗試存取記錄的資料庫中（例如連接到網際網路的資料庫-不必要的鎖定可能會快速導致應用程式的效能變慢）。  
  
 您可以藉由選擇適當的鎖定選項，來控制資料來源和 ADO 資料指標程式庫管理並行的方式。  
  
 在開啟**記錄集**之前設定**LockType**屬性，以指定提供者開啟它時應使用的鎖定類型。 讀取屬性，以傳回在開啟的**記錄集**物件上使用的鎖定類型。  
  
 提供者可能不支援所有的鎖定類型。 如果提供者無法支援所要求的**LockType**設定，則會取代另一種類型的鎖定。 若要判斷**記錄集**物件中可用的實際鎖定功能，請使用[支援](../../../ado/reference/ado-api/supports-method.md)方法搭配**adUpdate**和**adUpdateBatch**。  
  
 如果[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為 adUseClient，則不支援**adLockPessimistic**設定 **。** 如果設定了不支援的值，將不會產生錯誤;將改用最接近的支援**LockType** 。  
  
 當**記錄集**已關閉時， **LockType**屬性是讀取/寫入，而當它開啟時則為唯讀。  
  
 此章節包含下列主題。  
  
-   [鎖定的類型](../../../ado/guide/data/types-of-locks.md)
