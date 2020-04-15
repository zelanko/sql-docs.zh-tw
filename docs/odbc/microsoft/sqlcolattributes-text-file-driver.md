---
title: SQLColattributes(文字檔案驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], Text File Driver
ms.assetid: 132fd1c0-1921-4a7d-910e-aedf1bff5453
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3eafe02ba76dcaa6078abee862d743deb4765bdd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307919"
---
# <a name="sqlcolattributes-text-file-driver"></a>SQLColAttributes (文字檔驅動程式)
> [!NOTE]  
>  本主題提供特定於文本檔驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
|屬性|註解|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|對於 LONGVARBINARY 數據,SQL_COLUMN_DISPLAY_SIZE是列的最大長度,而不是列乘以 2 的最大長度。|  
|SQL_OWNER_NAME|此列中返回一個空字串 (""),因為不支援所有者名稱。|  
|SQL_QUALIFIER_NAME|返回目錄的路徑。|  
|SQL_COLUMN_SEARCHABLE|朗瓦里卡和朗瓦爾查爾列報告為SQL_UNSEARCHABLE。<br /><br /> 固定長度和可變長度二進位和字元資料類型是可搜索的,即使 LONGVARBINARY 和 LONGVARCHAR 不。|
