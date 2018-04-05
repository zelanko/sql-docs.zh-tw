---
title: SQLSpecialColumns （Visual FoxPro ODBC 驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 82e56af804ee91dd2231e8bf6baa141bd9f94115
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns （Visual FoxPro ODBC 驅動程式）
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援： 完整  
  
 ODBC 應用程式開發介面相容性： 層級 1  
  
 擷取最佳的資料行集可唯一識別資料表中的資料列。  
  
 Visual FoxPro ODBC 驅動程式會傳回構成 FoxPro 資料表的主索引鍵資料行。 (請參閱[SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)。)如果您的呼叫*fColType*設 SQL_ROWVER，會傳回任何資料行。 **SQLSpecialColumns**只適用於屬於資料來源[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)。  
  
 如需詳細資訊，請參閱[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md)中*ODBC 程式設計人員參考*。
