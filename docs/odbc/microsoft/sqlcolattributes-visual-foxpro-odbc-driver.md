---
description: SQLColAttributes (Visual FoxPro ODBC Driver)
title: SQLColAttributes (Visual FoxPro ODBC Driver) |Microsoft Docs
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
ms.openlocfilehash: 062a5af2e8aab4d71cf201284bd065242c588f6a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412194"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：核心層級  
  
 傳回結果集中資料行的描述項資訊。 描述項資訊會以字元字串、32位描述元相依值或整數值的形式傳回。  
  
> [!NOTE]  
>  **SQLColAttributes** 無法用來傳回書簽資料行 (資料行 0) 的相關資訊。  
  
 Visual FoxPro ODBC 驅動程式支援所有 *fDescType* 值。 下表包含驅動程式所選值的執行批註。  
  
|*fDescType*|註解|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|傳回 FALSE： Visual FoxPro 沒有計數器欄位。|  
|SQL_COLUMN_CASE_SENSITIVE|如果資料行類型是字元，一律會傳回 TRUE。|  
|SQL_COLUMN_LABEL|傳回 SQL_COLUMN_NAME 也會傳回的資料行名稱。|  
|SQL_COLUMN_MONEY|如果資料行類型是以 Visual FoxPro 語言) 中的 "Y" 表示的 Currency (，則傳回 TRUE。|  
|SQL_COLUMN_OWNER_NAME|永遠傳回空字串。|  
|SQL_COLUMN_QUALIFIER_NAME|永遠傳回空字串。|  
|SQL_COLUMN_SEARCHABLE|針對一般類型的資料行傳回 SQL_UNSEARCHABLE;這些資料行不能用在 WHERE 子句中。<br /><br /> 針對 NOCPTRANS 未設定的 Character 或 Memo 資料行傳回 SQL_SEARCHABLE;這些資料行可以在 WHERE 子句中搭配任何比較運算子使用。<br /><br /> 傳回所有其他資料行類型的 SQL_ALL_EXCEPT_LIKE;這些資料行可以用在 WHERE 子句中，除了 LIKE 以外的所有比較運算子。|  
|SQL_COLUMN_TABLE_NAME|永遠傳回空字串。|  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) 。
