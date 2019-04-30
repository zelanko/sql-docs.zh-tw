---
title: SQLEndTran （資料指標程式庫） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2e218035473d1ebb980aa5f44da8cc7b8ef843d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199496"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLEndTran**資料指標程式庫中的函式。 如需一般資訊**SQLEndTran**，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
 資料指標程式庫不支援交易，並將傳遞至呼叫**SQLEndTran**直接到驅動程式。 不過，資料指標程式庫所傳回的資料來源具有 SQL_CURSOR_ROLLBACK_BEHAVIOR 與 SQL_CURSOR_COMMIT_BEHAVIOR 資訊類型支援的資料指標的認可和回復行為：  
  
-   針對跨多筆交易中保留資料指標的資料來源，會回復資料來源中的變更會不回復資料指標程式庫的快取中。 若要讓比對資料來源中的資料的快取，應用程式必須關閉再重新開啟資料指標。  
  
-   關閉資料指標在交易界限的資料來源，資料指標程式庫會關閉資料指標，並刪除在此連接上的所有陳述式快取。  
  
-   刪除已備妥的陳述式在交易界限的資料來源，應用程式必須 reprepare 上的連接，再重新加以所有備妥的陳述式。
