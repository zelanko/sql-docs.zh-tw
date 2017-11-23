---
title: "SQLColAttributes 對應 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], mapping
ms.assetid: 30e25719-176b-4c48-97d4-920766b22412
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b342337838ced8fd4cb7976f703d9c4e85f985d0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqlcolattributes-mapping"></a>SQLColAttributes 對應
當應用程式呼叫**SQLColAttributes**透過 ODBC 3*.x*驅動程式，會呼叫**SQLColAttributes**對應至**SQLColAttribute** ，如下所示：  
  
> [!NOTE]  
>  使用中的前置詞*FieldIdentifier*值在 ODBC 3*.x*從該使用中的 ODBC 2 已變更。*x*。 新的前置詞為"SQL_DESC";舊的前置詞為"SQL_COLUMN"。  
  
1.  如果應用程式的 ODBC 2。*x*應用程式， *fDescType* SQL_COLUMN_TYPE，且傳回型別是精簡 DATETIME 類型，傳回值之日期、 時間和時間戳記代碼的驅動程式管理員對應。  
  
2.  如果*fDescType* SQL_COLUMN_NAME、 SQL_COLUMN_NULLABLE，或 SQL_COLUMN_COUNT，驅動程式管理員呼叫**SQLColAttribute**與驅動程式中*FieldIdentifier*引數對應到 SQL_DESC_NAME、 SQL_DESC_NULLABLE 或 SQL_DESC_COUNT，適當地*。* 所有其他的值*fDescType*會傳遞給驅動程式。  
  
 ODBC 3*.x*驅動程式必須支援所有 ODBC 3*.x* *FieldIdentifiers*列出**SQLColAttribute**。  
  
 ODBC 3*.x*驅動程式必須支援 SQL_COLUMN_PRECISION 和 SQL_DESC_PRECISION、 SQL_COLUMN_SCALE 和 SQL_DESC_SCALE，和 SQL_COLUMN_LENGTH 和 SQL_DESC_LENGTH。 這些值會不同，因為有效位數、 小數位數和長度會定義以不同的方式在 ODBC 3*.x*比 ODBC 2。*x*。 如需詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d： 資料型別中。
