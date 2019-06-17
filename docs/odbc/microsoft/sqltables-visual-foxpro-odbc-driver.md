---
title: SQLTables (Visual FoxPro ODBC Driver) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e134b2870c4506e725f2900b83d1118e42b55d15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63219114"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：完整  
  
 ODBC API 相容性：層級 1  
  
 傳回清單中的參數所指定的資料表名稱**SQLTables**陳述式。 如果未不指定任何參數，會傳回儲存在目前的資料來源中的資料表名稱。 驅動程式會傳回資訊當作結果集。  
  
 列舉型別呼叫將不會收到遠端檢視或本機的參數化的檢視的結果集項目。 不過，呼叫**SQLTables**與唯一的資料表名稱規範會發現這類檢視的相符項目如果存在具有該名稱，這可讓用來檢查是否有名稱衝突，再建立新的資料表 API。  
  
> [!NOTE]  
>  Visual FoxPro ODBC driver 區分[資料庫資料表](../../odbc/microsoft/visual-foxpro-terminology.md)並[免費資料表](../../odbc/microsoft/visual-foxpro-terminology.md)，即使這兩種類型的資料表會儲存在您的系統上相同的目錄。 如果您的資料來源是可用的資料表的目錄，Visual FoxPro ODBC Driver 不目錄或傳回與資料庫相關聯的任何資料表的名稱。  
  
 如需詳細資訊，請參閱 < [SQLTables](../../odbc/reference/syntax/sqltables-function.md)中*ODBC 程式設計人員參考*。
