---
title: "SQLGetInfo （文字檔案驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetInfo
ms.assetid: 6b7a630e-47f8-4ee1-b2a7-476bc1d0b0d4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4329838f20f6d832cbbc7576c23e35a51440ef95
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo （文字檔案驅動程式）
> [!NOTE]  
>  本主題提供文字檔驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLGetInfo**支援 SQL_FILE_USAGE 資訊類型。 傳回的值是 16 位元的整數，表示驅動程式如何直接處理的資料來源中的檔案：  
  
-   SQL_FILE_NOT_SUPPORTED — 驅動程式不是單層驅動程式。  
  
-   SQL_FILE_TABLE — 單層驅動程式將資料來源中的檔案視為資料表。  
  
-   SQL_FILE_QUALIFIER — 單層驅動程式辨識符號視為資料來源中的檔案。  
  
 ODBC 驅動程式會傳回 SQL_FILE_TABLE 如 Textdriver，因為每個檔案是資料表。  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|Version|版本號碼的格式|  
|----------|-------------|-------------------------------|  
|Text|1.0|01.00.0000|  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124;SQL_QU_TABLE_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; SQL_FN_TD_CURTIME &#124; SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124;SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124;SQL_FN_TD_MINUTE &#124;SQL_FN_TD_MONTH &#124; SQL_FN_TD_NOW &#124;SQL_FN_TD_SECOND &#124;SQL_FN_TD_WEEK &#124;SQL_FN_TD_YEAR

