---
title: SQL 特殊柱(可視化福克斯 Pro ODBC 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96b439674c8bda3494b4cefd0c1118602b537cd0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299378"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 符合性:1 級  
  
 檢索唯一標識表中行的最佳列集。  
  
 Visual FoxPro ODBC 驅動程式返回構成 FoxPro 表主鍵的列。 ( 請參考[SQL 主鍵](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)。如果使用*fColType*設置為 SQL_ROWVER調用,則不返回任何列。 **SQL特殊列只**對[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的數據源有效。  
  
 有關詳細資訊,請參閱*ODBC 程式師參考*中的[SQL 特殊列。](../../odbc/reference/syntax/sqlspecialcolumns-function.md)
