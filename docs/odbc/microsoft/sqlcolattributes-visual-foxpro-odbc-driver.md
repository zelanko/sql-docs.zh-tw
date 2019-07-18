---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9fb35211160cb7cba866c2b1c9b1cf72340e92ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132623"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：完整  
  
 ODBC API 相容性：核心層級  
  
 在結果集中傳回的資料行的描述項資訊。 為字元字串、 32 位元描述元相依值或整數值，會傳回描述元資訊。  
  
> [!NOTE]  
>  **SQLColAttributes**無法用來傳回書籤資料行 （資料行 0） 的相關資訊。  
  
 Visual FoxPro ODBC 驅動程式支援所有*fDescType*值。 下表包含所選值的驅動程式的實作上的註解。  
  
|*fDescType*|註解|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|會傳回 FALSE:Visual FoxPro 有任何計數器欄位。|  
|SQL_COLUMN_CASE_SENSITIVE|如果資料行類型是字元，一律會傳回 TRUE。|  
|SQL_COLUMN_LABEL|傳回的資料行名稱，它也會傳回 SQL_COLUMN_NAME。|  
|SQL_COLUMN_MONEY|為 true，則會傳回資料行的類型如果是貨幣 （由 Visual FoxPro 語言中的"Y"）。|  
|SQL_COLUMN_OWNER_NAME|一律會傳回空字串。|  
|SQL_COLUMN_QUALIFIER_NAME|一律會傳回空字串。|  
|SQL_COLUMN_SEARCHABLE|傳回 SQL_UNSEARCHABLE 一般; 類型的資料行這些資料行不能在 WHERE 子句。<br /><br /> 類型字元或使用 NOCPTRANS 的附註的資料行傳回 SQL_SEARCHABLE 未設定;這些資料行可以用於 WHERE 子句搭配任何比較運算子。<br /><br /> 對於所有其他資料行類型; 傳回 SQL_ALL_EXCEPT_LIKE這些資料行可以用於 WHERE 子句使用類似以外的所有比較運算子。|  
|SQL_COLUMN_TABLE_NAME|一律會傳回空字串。|  
  
 如需詳細資訊，請參閱 < [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md)中*ODBC 程式設計人員參考*。
