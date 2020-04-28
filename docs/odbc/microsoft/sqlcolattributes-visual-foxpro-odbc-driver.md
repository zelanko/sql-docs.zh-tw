---
title: SQLColAttributes （Visual FoxPro ODBC Driver） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307909"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：核心層級  
  
 傳回結果集中資料行的描述項資訊。 描述元資訊會以字元字串、32位描述項相依值或整數值的形式傳回。  
  
> [!NOTE]  
>  **SQLColAttributes**不能用來傳回書簽資料行（資料行0）的相關資訊。  
  
 Visual FoxPro ODBC 驅動程式支援所有的*fDescType*值。 下表包含驅動程式所選值的執行批註。  
  
|*fDescType*|註解|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|傳回 FALSE： Visual FoxPro 沒有計數器欄位。|  
|SQL_COLUMN_CASE_SENSITIVE|如果資料行類型是字元，一律會傳回 TRUE。|  
|SQL_COLUMN_LABEL|傳回資料行名稱，這也會由 SQL_COLUMN_NAME 傳回。|  
|SQL_COLUMN_MONEY|如果資料行類型是貨幣（以 Visual FoxPro 語言中的 "Y" 表示），則傳回 TRUE。|  
|SQL_COLUMN_OWNER_NAME|永遠傳回空字串。|  
|SQL_COLUMN_QUALIFIER_NAME|永遠傳回空字串。|  
|SQL_COLUMN_SEARCHABLE|針對一般類型的資料行傳回 SQL_UNSEARCHABLE。在 WHERE 子句中不能使用這些資料行。<br /><br /> 針對 NOCPTRANS 未設定的字元或備忘類型的資料行傳回 SQL_SEARCHABLE;這些資料行可以在 WHERE 子句中搭配任何比較運算子使用。<br /><br /> 傳回所有其他資料行類型的 SQL_ALL_EXCEPT_LIKE;這些資料行可以用在 WHERE 子句中，並搭配所有比較運算子（例如）。|  
|SQL_COLUMN_TABLE_NAME|永遠傳回空字串。|  
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) 。
