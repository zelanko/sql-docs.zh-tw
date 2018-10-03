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
manager: craigg
ms.openlocfilehash: 981b2b5dc1f76d879b18e5569e7fb70dbece1538
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813076"
---
# <a name="what-is-a-lock"></a>什麼是鎖定？
鎖定是 DBMS 會存取限制多使用者環境中的資料列的程序。 資料列或資料行以獨佔方式鎖定時，不允許其他使用者存取已鎖定的資料，直到釋放鎖定為止。 這可確保兩位使用者無法同時更新相同資料列中的資料行。  
  
 鎖定可能會耗費資源的觀點，並應只在需要時保留資料完整性。 其中數百或數千位使用者可能嘗試存取記錄每秒的資料庫中，例如資料庫連線到網際網路，在您的應用程式的效能變慢可能很快會造成不必要的鎖定。  
  
 您可以控制如何在資料來源和 ADO 資料指標程式庫管理並行存取選擇適當的鎖定選項。  
  
 設定**LockType**屬性，才能開啟**資料錄集**指定開啟它時，應該使用的鎖定提供者類型。 讀取屬性的傳回類型的鎖定上開啟的使用中**資料錄集**物件。  
  
 提供者可能不支援所有的鎖定類型。 如果提供者無法支援要求**LockType**設定，它會取代另一種類型的鎖定。 若要判斷中可用的實際鎖定功能**資料錄集**物件，請使用[支援](../../../ado/reference/ado-api/supports-method.md)方法**adUpdate**並**adUpdateBatch**.  
  
 **Locktype**如果，則不支援設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient。** 如果設定不支援的值，不會產生錯誤;設定支援的最接近**LockType**將改為使用。  
  
 **LockType**屬性是讀取/寫入時**資料錄集**開啟時，會關閉，且為唯讀狀態。  
  
 此章節包含下列主題。  
  
-   [鎖定的類型](../../../ado/guide/data/types-of-locks.md)
