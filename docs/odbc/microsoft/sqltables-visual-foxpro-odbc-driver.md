---
title: SQLTables(可視化福克斯Pro ODBC驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5467fc8c1717d5ceb548b3950a0894fd2a1b4499
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299279"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 符合性:1 級  
  
 傳回**SQLTables**敘述中參數指定的表格名稱的清單。 如果未指定參數,則返回存儲在當前數據源中的表名稱。 驅動程式將返回結果集。  
  
 枚舉類型調用將不會接收遠端檢視或本地參數化檢視的結果集條目。 但是,如果存在具有該名稱的**SQLTables,** 則使用唯一表名稱指定器的調用將找到此類視圖的匹配項;這允許在創建新表之前使用 API 檢查名稱衝突。  
  
> [!NOTE]  
>  Visual FoxPro ODBC 驅動程式區分[資料庫表](../../odbc/microsoft/visual-foxpro-terminology.md)和[可用表](../../odbc/microsoft/visual-foxpro-terminology.md),即使這兩種類型的表都存儲在系統上的同一目錄中。 如果數據來源是可用表的目錄,則 Visual FoxPro ODBC 驅動程式不會編目或傳回與資料庫關聯的任何表的名稱。  
  
 有關詳細資訊,請參閱*ODBC 程式師參考中的* [SQLTables。](../../odbc/reference/syntax/sqltables-function.md)
