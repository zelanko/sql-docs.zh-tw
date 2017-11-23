---
title: "SQLPrimaryKeys （Visual FoxPro ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e0d7c874fe97f70f5e8d8096a4b03a2f064f2cb1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys （Visual FoxPro ODBC 驅動程式）
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援： 完整  
  
 ODBC 應用程式開發介面相容性： 層級 2  
  
 傳回組成資料表主索引鍵資料行名稱。 Visual FoxPro ODBC 驅動程式實作**SQLPrimaryKeys**行為，如下所示：  
  
-   會忽略*szTableOwner*和*cbTableOwner*引數。  
  
-   僅適用於屬於資料來源[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)。 驅動程式會傳回錯誤 「 驅動程式不支援此函式"如果資料來源的目錄[釋放資料表](../../odbc/microsoft/visual-foxpro-terminology.md)。  
  
 如需詳細資訊，請參閱[SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md)中*ODBC 程式設計人員參考*。
