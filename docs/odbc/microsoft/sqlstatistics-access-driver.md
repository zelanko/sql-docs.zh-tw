---
title: "SQLStatistics （存取驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Access Driver
ms.assetid: 6117ac77-1020-4f0c-8eed-e671c34c1f21
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b40732d6e9f4e6c4af3b857ce18ce50b9991a0c6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics （存取驅動程式）
> [!NOTE]  
>  本主題提供存取驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|資料行|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|會傳回 Microsoft Access 資料庫檔案的路徑。<br /><br /> 模式比對中不支援*szTableQualifier*引數。|  
|TABLE_OWNER|因為擁有者名稱不支援此資料行，就會傳回 NULL。|  
|TABLE_NAME|未分隔的資料表名稱。<br /><br /> 模式比對中不支援*szTableName*引數。|  
|INDEX_QUALIFIER|一律傳回 NULL。|  
|INDEX_NAME|索引而定。|  
|TYPE|只有 SQL_TABLE_STAT 或 SQL_INDEX_OTHER 就會傳回型別。|  
|SEQ_IN_INDEX|索引而定。|  
|COLUMN_NAME|索引而定。|  
|COLLATION|索引而定。|  
|CARDINALITY|只針對 Microsoft Access 傳回。|  
|PAGES|一律傳回 NULL。|  
  
 篩選根據唯一性 ( *fUnique*引數)。 *FAccuracy*參數已忽略。

