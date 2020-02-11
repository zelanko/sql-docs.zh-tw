---
title: SQLGetInfo （文字檔驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetInfo
ms.assetid: 6b7a630e-47f8-4ee1-b2a7-476bc1d0b0d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 892fdabc319b1d495120cdce20d77f05cd232418
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898824"
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 **SQLGetInfo**支援 SQL_FILE_USAGE 資訊類型。 傳回的值是16位整數，表示驅動程式如何直接處理資料來源中的檔案：  
  
-   SQL_FILE_NOT_SUPPORTED-驅動程式不是一層式驅動程式。  
  
-   SQL_FILE_TABLE-一層式驅動程式會將資料來源中的檔案視為資料表。  
  
-   SQL_FILE_QUALIFIER-一層式驅動程式會將資料來源中的檔案視為辨識符號。  
  
 ODBC 驅動程式會傳回 Textdriver SQL_FILE_TABLE，因為每個檔案都是一個資料表。  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|ISAM|版本|版本號碼的格式|  
|----------|-------------|-------------------------------|  
|Text|1.0|01.00.0000|  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; SQL_FN_TD_CURTIME &#124; SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_NOW &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
