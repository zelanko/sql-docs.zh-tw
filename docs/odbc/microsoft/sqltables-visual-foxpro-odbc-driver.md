---
title: SQLTables （Visual FoxPro ODBC Driver） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5467fc8c1717d5ceb548b3950a0894fd2a1b4499
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299279"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：層級1  
  
 傳回**SQLTables**語句中的參數所指定的資料表名稱清單。 如果未指定任何參數，則會傳回儲存在目前資料來源中的資料表名稱。 驅動程式會以結果集的形式傳回信息。  
  
 列舉類型呼叫將不會收到遠端查看或本機參數化視圖的結果集專案。 不過，以唯一資料表名稱規範呼叫**SQLTables**時，會發現這類視圖的相符情況，如果有該名稱存在，這可讓 API 用來檢查建立新資料表之前的名稱衝突。  
  
> [!NOTE]  
>  Visual FoxPro ODBC 驅動程式會區分[資料庫資料表](../../odbc/microsoft/visual-foxpro-terminology.md)和[可用的資料表](../../odbc/microsoft/visual-foxpro-terminology.md)，即使兩種類型的資料表都儲存在系統的相同目錄中。 如果您的資料來源是可用資料表的目錄，Visual FoxPro ODBC 驅動程式不會目錄或傳回與資料庫相關聯之任何資料表的名稱。  
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLTables](../../odbc/reference/syntax/sqltables-function.md) 。
