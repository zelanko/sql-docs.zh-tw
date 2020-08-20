---
description: SQLColAttributes 對應
title: SQLColAttributes 對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], mapping
ms.assetid: 30e25719-176b-4c48-97d4-920766b22412
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 864f81877e548de9bbb0478e9313c2cd38dd3838
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466039"
---
# <a name="sqlcolattributes-mapping"></a>SQLColAttributes 對應
當應用程式*透過 ODBC 3.x 驅動程式呼叫* **SQLColAttributes**時， **SQLColAttributes**的呼叫會對應至**SQLColAttribute** ，如下所示：  
  
> [!NOTE]
>  ODBC 3.x 中用於*FieldIdentifier*值的前置*詞已從*odbc 2.x 中使用的前置詞變更 *。* 新的前置詞為 "SQL_DESC";舊的前置詞為 "SQL_COLUMN"。  
  
1.  如果 *應用程式是 ODBC 2.x* 應用程式，則會 SQL_COLUMN_TYPE *fDescType* ，而傳回的型別是精確的日期時間類型，驅動程式管理員會對應日期、時間和時間戳記代碼的傳回值。  
  
2.  如果 *fDescType* 為 SQL_COLUMN_NAME、SQL_COLUMN_NullABLE 或 SQL_COLUMN_COUNT，驅動程式管理員會在驅動程式中呼叫 **SQLColAttribute** ，並視需要將 *FieldIdentifier* 引數對應至 SQL_DESC_NAME、SQL_DESC_NullABLE 或 SQL_DESC_COUNT *。* *FDescType*的所有其他值都會傳遞至驅動程式。  
  
 ODBC 3.x*驅動程式*必須支援針對**SQLColAttribute**列出的所有*3.x* odbc 3.x *FieldIdentifiers* 。  
  
 *ODBC 3.x*驅動程式必須支援 SQL_COLUMN_PRECISION 和 SQL_DESC_PRECISION、SQL_COLUMN_SCALE 和 SQL_DESC_SCALE，以及 SQL_COLUMN_LENGTH 和 SQL_DESC_LENGTH。 這些值會不同，因為*在 odbc 3.x*中的精確度、小數位數和長度的定義方式 *，與 odbc* 2.x 中的定義不同。 如需詳細資訊，請參閱附錄 D：資料類型中的資料 [行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 。
