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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923446"
---
# <a name="what-is-a-lock"></a>什麼是鎖定？
鎖定是 DBMS 會存取限制多使用者環境中的資料列的程序。 資料列或資料行以獨佔方式鎖定時，不允許其他使用者存取已鎖定的資料，直到釋放鎖定為止。 這可確保兩位使用者無法同時更新相同資料列中的資料行。  
  
 鎖定可能會耗費資源的觀點，並應只在需要時保留資料完整性。 在其中數百或數千位使用者可能嘗試存取記錄每秒-例如連線到網際網路-資料庫的資料庫不必要的鎖定無法快速產生應用程式中的效能變慢。  
  
 您可以控制如何在資料來源和 ADO 資料指標程式庫管理並行存取選擇適當的鎖定選項。  
  
 設定**LockType**屬性，才能開啟**資料錄集**指定開啟它時，應該使用的鎖定提供者類型。 讀取屬性的傳回類型的鎖定上開啟的使用中**資料錄集**物件。  
  
 提供者可能不支援所有的鎖定類型。 如果提供者無法支援要求**LockType**設定，它會取代另一種類型的鎖定。 若要判斷中可用的實際鎖定功能**資料錄集**物件，請使用[支援](../../../ado/reference/ado-api/supports-method.md)方法**adUpdate**並**adUpdateBatch**.  
  
 **Locktype**如果，則不支援設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient。** 如果設定不支援的值，不會產生錯誤;設定支援的最接近**LockType**將改為使用。  
  
 **LockType**屬性是讀取/寫入時**資料錄集**開啟時，會關閉，且為唯讀狀態。  
  
 此章節包含下列主題。  
  
-   [鎖定的類型](../../../ado/guide/data/types-of-locks.md)
