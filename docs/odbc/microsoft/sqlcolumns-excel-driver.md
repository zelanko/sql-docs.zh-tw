---
title: SQL柱(Excel 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColumns function [ODBC], Excel Driver
- Excel driver [ODBC], SQLColumns
ms.assetid: 4bae3fcd-0287-4f79-ad7c-8f7ab2f6f940
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c168168e0cb44d6aff2102bb18c07cbf1a1953a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307879"
---
# <a name="sqlcolumns-excel-driver"></a>SQLColumns (Excel 驅動程式)
> [!NOTE]  
>  本主題提供特定於 Excel 驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
|資料行|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|返回目錄的路徑。|  
|TABLE_OWNER|由於不支援擁有者名稱,因此在此列中返回 NULL。|  
|NULLABLE|對於參與主鍵或唯一索引的列,將返回SQL_NO_NULLS。|
