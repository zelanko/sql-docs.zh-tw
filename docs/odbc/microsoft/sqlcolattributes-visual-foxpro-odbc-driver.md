---
title: SQLColattributes(可視化狐狸Pro ODBC驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: d403dfa0-c26d-47d4-91d9-2f29aa387399
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9508fa7b9ada8273e1250d7584e577892acf5c51
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307909"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 一致性:核心等級  
  
 返回結果集中列的描述符資訊。 描述符資訊將作為字串、32 位描述符相關值或整數值返回。  
  
> [!NOTE]  
>  **SQLColAttributes**不能用於返回有關書籤列(列 0)的資訊。  
  
 可視化 FoxPro ODBC 驅動程式支援所有*fDescType*值。 下表包括有關驅動程序實現選定值的註釋。  
  
|*fDescType*|註解|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|返回 FALSE: 可視化 FoxPro 沒有計數器欄位。|  
|SQL_COLUMN_CASE_SENSITIVE|如果列類型為"字元",則始終返回 TRUE。|  
|SQL_COLUMN_LABEL|返回列名稱,該列名稱也由SQL_COLUMN_NAME返回。|  
|SQL_COLUMN_MONEY|如果列類型為貨幣(由 Visual FoxPro 語言中的"Y"表示)則返回 TRUE。|  
|SQL_COLUMN_OWNER_NAME|永遠傳回空字串。|  
|SQL_COLUMN_QUALIFIER_NAME|永遠傳回空字串。|  
|SQL_COLUMN_SEARCHABLE|返回「常規」類型的列SQL_UNSEARCHABLE;這些列不能在 WHERE 子句中使用。<br /><br /> 返回未設置 NOCPTRANS 的類型「字元」或「備忘錄」的列SQL_SEARCHABLE;這些列可以在 WHERE 子句中與任何比較運算符一起使用。<br /><br /> 返回所有其他列類型的SQL_ALL_EXCEPT_LIKE;這些列可以在 WHERE 子句中使用,除 LIKE 之外,所有比較運算符除外。|  
|SQL_COLUMN_TABLE_NAME|永遠傳回空字串。|  
  
 有關詳細資訊,請參閱*ODBC 程式師參考*中的[SQLColattributes。](../../odbc/reference/syntax/sqlcolattributes-function.md)
