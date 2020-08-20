---
description: SQLEndTran (資料指標程式庫)
title: SQLEndTran (資料指標程式庫) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25584f19a885580be24b2681ccd639de285fb4b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466030"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLEndTran** 函數。 如需 **SQLEndTran**的一般資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
 資料指標程式庫不支援交易，而會將呼叫直接傳遞至驅動程式 **SQLEndTran** 。 但是，資料指標程式庫確實支援資料來源傳回的資料指標認可和回復行為，並具有 SQL_CURSOR_ROLLBACK_BEHAVIOR 和 SQL_CURSOR_COMMIT_BEHAVIOR 資訊類型：  
  
-   對於跨交易保留資料指標的資料來源，在資料來源中復原的變更不會在資料指標程式庫的快取中復原。 若要讓快取符合資料來源中的資料，應用程式必須關閉並重新開啟資料指標。  
  
-   針對在交易界限關閉資料指標的資料來源，資料指標程式庫會關閉資料指標，並刪除連接上所有語句的快取。  
  
-   針對在交易界限刪除備妥語句的資料來源，應用程式必須先 reprepare 連接上所有備妥的語句，然後再暫停它們。
