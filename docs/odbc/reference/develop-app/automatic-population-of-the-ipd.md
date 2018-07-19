---
title: 自動母體擴展的 IPD |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatically populating ipd [ODBC]
- descriptors [ODBC], automatically populating ipd
- descriptors [ODBC], allocating and freeing
- ipd [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1184a7d8-d557-4140-843b-6633ae6deacc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9e3d80ea280e4487f5443bca8152a3a541dfbd8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908353"
---
# <a name="automatic-population-of-the-ipd"></a>IPD 中的自動擴展
有些驅動程式都能參數化的查詢已備妥之後，設定 IPD 欄位。 描述項欄位會自動填入參數，包括資料類型、 有效位數、 小數位數和其他特性的相關資訊。 這相當於支援**SQLDescribeParam**。 當它有沒有其他方法來探索它，例如臨機操作查詢執行的應用程式不知道參數時，這項資訊可以是尤其有價值的應用程式。  
  
 應用程式會決定此驅動程式是否支援自動母體擴展，藉由呼叫**SQLGetConnectAttr**與*屬性*SQL_ATTR_AUTO_IPD。 如果傳回 SQL_TRUE，則此驅動程式支援它，應用程式可以將 SQL_ATTR_ENABLE_AUTO_IPD 陳述式屬性設定為 SQL_TRUE 來啟用它。  
  
 已備妥 SQL 陳述式包含參數標記呼叫之後，驅動程式時自動母體擴展是支援，而且已啟用，擴展 IPD 欄位**SQLPrepare**。 應用程式可以擷取這項資訊藉由呼叫**SQLGetDescField**或**SQLGetDescRec**，或**SQLDescribeParam**。 參數的最適當的應用程式緩衝區繫結，或為其指定的資料轉換，應用程式可以使用資訊。  
  
 IPD 中的自動母體擴展可能會產生對效能帶來負面影響。 應用程式可以將它關閉正在 SQL_ATTR_ENABLE_AUTO_IPD 陳述式屬性重設為 SQL_FALSE （預設值）。
