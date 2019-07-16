---
title: 自動填入 IPD |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- automatically populating ipd [ODBC]
- descriptors [ODBC], automatically populating ipd
- descriptors [ODBC], allocating and freeing
- ipd [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1184a7d8-d557-4140-843b-6633ae6deacc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1591843667ef01c6c88f5dfafb734f044679b2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909834"
---
# <a name="automatic-population-of-the-ipd"></a>自動 IPD 擴展
有些驅動程式是可參數化的查詢已備妥之後，請設定 IPD 欄位。 描述項欄位會自動填入參數，包括資料類型、 有效位數、 小數位數和其他特性的相關資訊。 這相當於支援**SQLDescribeParam**。 當它有沒有其他方法來探索它，例如隨選查詢執行的應用程式不知道的參數時，這項資訊可以是非常有價值的應用程式。  
  
 應用程式可讓您判斷驅動程式是否支援自動母體擴展，藉由呼叫**SQLGetConnectAttr**具有*屬性*SQL_ATTR_AUTO_IPD。 如果傳回 SQL_TRUE，驅動程式支援及應用程式可以設定為 SQL_TRUE 的 SQL_ATTR_ENABLE_AUTO_IPD 陳述式屬性來啟用它。  
  
 已備妥 SQL 陳述式包含參數標記呼叫之後，驅動程式時支援自動母體擴展，且已啟用，填入 IPD 欄位**SQLPrepare**。 應用程式可以擷取這項資訊藉由呼叫**SQLGetDescField**或是**SQLGetDescRec**，或**SQLDescribeParam**。 參數的最適當的應用程式緩衝區繫結，或為其指定的資料轉換，應用程式可以使用資訊。  
  
 自動 IPD 擴展可能會產生對效能帶來負面影響。 應用程式可以將它關閉 SQL_ATTR_ENABLE_AUTO_IPD 陳述式屬性重設 SQL_FALSE （預設值）。
