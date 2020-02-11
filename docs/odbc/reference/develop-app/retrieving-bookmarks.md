---
title: 正在抓取書簽 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f18b87adf31f19d2a93bb3af3e14c265ae3940af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020570"
---
# <a name="retrieving-bookmarks"></a>擷取書籤
如果應用程式將使用書簽，則在準備或執行語句之前，必須先將 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE。 這是必要的，因為建立和維護書簽可能是昂貴的作業，因此只有當應用程式可以充分使用書簽時，才應該啟用它們。  
  
 書簽會當做結果集的資料行0傳回。 有三種方式可供應用程式取得：  
  
-   系結結果集的資料行0。 **SQLFetch**或**SQLFetchScroll**會傳回資料列集內每個資料列的書簽，以及其他系結資料行的資料。  
  
-   呼叫**SQLSetPos**以定位至資料列集中的資料列，然後針對資料行0呼叫**SQLGetData** 。 如果驅動程式支援書簽，它一定會支援對資料行0呼叫**SQLGetData**的能力，即使它不允許應用程式針對最後一個系結資料行之前的其他資料行呼叫**SQLGetData**也一樣。  
  
-   呼叫**SQLBulkOperations** ，並將*Operation*引數設定為 SQL_ADD，並將資料行0系結。 資料指標會插入資料列，並傳回系結緩衝區中資料列的書簽。
