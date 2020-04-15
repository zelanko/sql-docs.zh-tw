---
title: SQL柱(文字檔案驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLColumns
- SQLColumns function [ODBC], Text File Driver
ms.assetid: c99e5f8d-4e43-48f8-9e0e-086707b411f5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78c2e20f12dedf399ab36dd908f83aa93bebffc4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307862"
---
# <a name="sqlcolumns-text-file-driver"></a>SQLColumns (文字檔驅動程式)
> [!NOTE]  
>  本主題提供特定於文本檔驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
|資料行|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|返回目錄的路徑。|  
|TABLE_OWNER|由於不支援擁有者名稱,因此在此列中返回 NULL。|  
|NULLABLE|對於參與主鍵或唯一索引的列,將返回SQL_NO_NULLS。|
