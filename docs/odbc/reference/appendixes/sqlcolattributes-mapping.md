---
title: SQLColattributes 映射 |微軟文件
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
ms.openlocfilehash: 5c2c8386d6771141eaa0145a5d5964d70d6084d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305414"
---
# <a name="sqlcolattributes-mapping"></a>SQLColAttributes 對應
當應用程式透過 ODBC *3.x*驅動程式呼叫**SQLColAttributes**時,對**SQLColAttributes**的呼叫將映射到**SQLColAttribute,** 如下所示:  
  
> [!NOTE]
>  ODBC *3.x*中*字段識別符*值中使用的前置碼已更改,與 ODBC *2.x*中使用的前置碼相比。 新首碼為"SQL_DESC";新首碼為"SQL_DESC";如果 "SQL_DESC",則為"SQL_DESC"舊首碼為"SQL_COLUMN"  
  
1.  如果應用程式是 ODBC *2.x*應用程式,*則 fDescType*是SQL_COLUMN_TYPE,並且傳回的類型是簡潔的 DATETIME 類型,則驅動程式管理器映射日期、時間和時間戳代碼的傳回值。  
  
2.  如果*fDescType*是SQL_COLUMN_NAME、SQL_COLUMN_NULLABLE 或SQL_COLUMN_COUNT,則驅動程式管理器在驅動程式中呼叫**SQLColAttribute,** 並根據需要將*字段標識符*參數映射到SQL_DESC_NAME、SQL_DESC_NULLABLE或*SQL_DESC_COUNT。* *fDescType*的所有其他值都傳遞給驅動程式。  
  
 ODBC *3.x*驅動程式必須支援為**SQLColAttribute**列出的所有 ODBC *3.x* *欄位識別碼*。  
  
 ODBC *3.x*驅動程式必須支援SQL_COLUMN_PRECISION和SQL_DESC_PRECISION、SQL_COLUMN_SCALE和SQL_DESC_SCALE以及SQL_COLUMN_LENGTH和SQL_DESC_LENGTH。 這些值不同,因為在 ODBC *3.x*中定義的精度、比例和長度與 ODBC *2.x*中的定義不同。 有關詳細資訊,請參閱附錄 D 中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md):資料類型。
