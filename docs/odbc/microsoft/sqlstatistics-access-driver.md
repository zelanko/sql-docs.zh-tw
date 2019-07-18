---
title: SQLStatistics （Access 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Access Driver
ms.assetid: 6117ac77-1020-4f0c-8eed-e671c34c1f21
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 523f44924858af182e953aa1ce2b72e20cf97a45
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047085"
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|「資料行」|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|會傳回 Microsoft Access 資料庫檔案的路徑。<br /><br /> 模式比對中不支援*szTableQualifier*引數。|  
|TABLE_OWNER|在本專欄中，會傳回 NULL，因為不支援擁有者名稱。|  
|TABLE_NAME|分隔的資料表名稱。<br /><br /> 模式比對中不支援*szTableName*引數。|  
|INDEX_QUALIFIER|永遠傳回 NULL。|  
|INDEX_NAME|索引相關。|  
|TYPE|只有 SQL_TABLE_STAT 或 SQL_INDEX_OTHER 就會傳回型別。|  
|SEQ_IN_INDEX|索引相關。|  
|COLUMN_NAME|索引相關。|  
|COLLATION|索引相關。|  
|CARDINALITY|僅針對 Microsoft Access 傳回。|  
|PAGES|永遠傳回 NULL。|  
  
 篩選根據唯一性 ( *fUnique*引數)。 *FAccuracy*參數會被忽略。
