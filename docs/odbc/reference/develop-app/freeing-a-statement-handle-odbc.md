---
description: 釋放陳述式控制代碼 ODBC
title: 釋放語句控制碼 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d199d00c007abc6836755f5a78e93e3fd85b140b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461460"
---
# <a name="freeing-a-statement-handle-odbc"></a>釋放陳述式控制代碼 ODBC
如先前所述，重複使用語句比卸載它們並配置新語句更有效率。 在語句上執行新的 SQL 語句之前，應用程式應該確定目前的語句設定是否適當。 這些包括陳述式屬性、參數繫結，以及結果集繫結。 一般而言，舊 SQL 語句的參數和結果集會 (藉由使用 SQL_RESET_PARAMS 來呼叫 **SQLFreeStmt** ，並 SQL_UNBIND 選項) 和重新系結新的 sql 語句來解除系結。  
  
 當應用程式完成使用語句時，它會呼叫 **SQLFreeHandle** 來釋放語句。 釋放語句之後，在呼叫 ODBC 函數時，就會使用語句的控制碼來進行應用程式程式設計錯誤;這樣做會有未定義但可能會產生嚴重的後果。  
  
 當呼叫 **SQLFreeHandle** 時，驅動程式會釋放用來儲存語句相關資訊的結構。  
  
 **SQLDisconnect** 會自動釋出連接上的所有語句。
