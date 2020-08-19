---
description: 擷取書籤
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22fba0ccc900d221e915fea939736aa87b101e80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429090"
---
# <a name="retrieving-bookmarks"></a>擷取書籤
如果應用程式將使用書簽，則在準備或執行語句之前，它必須將 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE。 這是必要的，因為建立和維護書簽可能是昂貴的作業，因此只有當應用程式可以充分利用書簽時，才應該啟用。  
  
 書簽會以資料行0的形式傳回結果集。 有三種方式可供應用程式取出：  
  
-   系結結果集的資料行0。 **SQLFetch** 或 **SQLFetchScroll** 會傳回資料列集中每個資料列的書簽，以及其他系結資料行的資料。  
  
-   呼叫 **SQLSetPos** 以定位至資料列集中的資料列，然後呼叫資料行0的 **SQLGetData** 。 如果驅動程式支援書簽，它一定會支援對資料行0呼叫 **SQLGetData** 的能力，即使它不允許應用程式在最後一個系結資料行之前呼叫其他資料行的 **SQLGetData** 也是一樣。  
  
-   呼叫 **SQLBulkOperations** ，並將 *Operation* 引數設定為 SQL_ADD，並將資料行0系結。 資料指標會插入資料列，並傳回系結緩衝區中資料列的書簽。
