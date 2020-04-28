---
title: IPD 的自動填入 |Microsoft Docs
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
ms.openlocfilehash: 1998ea1992ee7f14d87d01e348d955b017166088
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285068"
---
# <a name="automatic-population-of-the-ipd"></a>自動 IPD 擴展
有些驅動程式可以在準備參數化查詢之後，設定 IPD 的欄位。 [描述項] 欄位會自動填入參數的相關資訊，包括資料類型、有效位數、小數位數和其他特性。 這相當於支援**SQLDescribeParam**。 當應用程式沒有其他方法可進行探索時，這類資訊可能特別有用，例如當使用應用程式不知道的參數執行臨機操作查詢時。  
  
 應用程式會藉由使用 SQL_ATTR_AUTO_IPD 的*屬性*來呼叫**SQLGetConnectAttr** ，以判斷驅動程式是否支援自動填入。 如果傳回 SQL_TRUE，驅動程式就會支援它，而且應用程式可以藉由將 SQL_ATTR_ENABLE_AUTO_IPD 語句屬性設定為 SQL_TRUE 來啟用它。  
  
 當支援並啟用自動填入時，驅動程式會在包含參數標記的 SQL 語句已由呼叫**SQLPrepare**準備好之後，填入 IPD 的欄位。 應用程式可以藉由呼叫**SQLGetDescField**或**SQLGetDescRec**，或**SQLDescribeParam**來抓取這項資訊。 應用程式可以使用此資訊來系結參數的最適當應用程式緩衝區，或為它指定資料轉換。  
  
 自動填入 IPD 可能會產生效能上的負面影響。 應用程式可以將 SQL_ATTR_ENABLE_AUTO_IPD 語句屬性重設為 SQL_FALSE （預設值），將它關閉。
