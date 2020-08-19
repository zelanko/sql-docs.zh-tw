---
description: 自動 IPD 擴展
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73c0456f1c78ccc19f1ff55a1ab288baedae2e14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476880"
---
# <a name="automatic-population-of-the-ipd"></a>自動 IPD 擴展
某些驅動程式可以在已準備參數化查詢之後，設定 IPD 的欄位。 描述項欄位會自動填入參數的相關資訊，包括資料類型、精確度、小數位數和其他特性。 這相當於支援 **SQLDescribeParam**。 當應用程式沒有其他方法可探索時，這項資訊可能特別有用，例如當隨選查詢使用應用程式不知道的參數執行特定查詢時。  
  
 應用程式會藉由呼叫 SQL_ATTR_AUTO_IPD*屬性*的**SQLGetConnectAttr** ，判斷驅動程式是否支援自動擴展。 如果傳回 SQL_TRUE，驅動程式就會支援它，而且應用程式可以將 SQL_ATTR_ENABLE_AUTO_IPD 語句屬性設定為 SQL_TRUE 來啟用它。  
  
 當支援並啟用自動擴展時，驅動程式會在呼叫 **SQLPrepare**來備妥包含參數標記的 SQL 語句之後，填入 IPD 的欄位。 應用程式可以藉由呼叫 **SQLGetDescField** 或 **SQLGetDescRec**或 **SQLDescribeParam**來取得此資訊。 應用程式可以使用此資訊來系結參數最適當的應用程式緩衝區，或為其指定資料轉換。  
  
 自動填入 IPD 可能會產生效能上的負面影響。 應用程式可以將 SQL_ATTR_ENABLE_AUTO_IPD 語句屬性重設為 SQL_FALSE (預設值) 來將它關閉。
