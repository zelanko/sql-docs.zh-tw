---
title: SQLPrimaryKeys (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3eeafa338fea31741609e6f9a9b32a4128ebd87d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62636327"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：完整  
  
 ODBC API 相容性：層級 2  
  
 傳回包含資料表的主索引鍵資料行名稱。 Visual FoxPro ODBC Driver 實作**SQLPrimaryKeys**行為，如下所示：  
  
-   會忽略*szTableOwner*並*cbTableOwner*引數。  
  
-   僅適用於資料來源[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)。 驅動程式會傳回錯誤 「 驅動程式不支援此函式 」 的目錄資料來源是否[免費資料表](../../odbc/microsoft/visual-foxpro-terminology.md)。  
  
 如需詳細資訊，請參閱 < [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md)中*ODBC 程式設計人員參考*。
