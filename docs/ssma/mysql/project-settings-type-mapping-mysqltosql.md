---
title: "專案設定 （型別對應） (MySQLToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 136fdf6d-657f-447b-af41-49bbc6e0e93e
caps.latest.revision: "13"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 00caaddad937894b416e3289a7d4e96b152ac41b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="project-settings-type-mapping-mysqltosql"></a>專案設定 （型別對應） (MySQLToSQL)
型別對應的專案設定可讓您設定的 SSMA 專案的預設型別對應。  

型別對應是可用的專案設定和預設專案設定 對話方塊中：  
  
-   使用 [專案設定] 對話方塊，設定目前專案的組態選項。 若要存取 [工具] 功能表上的型別對應設定選取專案設定，然後按一下類型對應的左窗格中。  
  
-   您可以使用預設專案設定 對話方塊來設定所有專案的組態選項。 若要存取的類型對應設定，請在 工具 功能表中，選取預設專案設定，設定會才能檢視 / 變更從選取的移轉專案類型**移轉的目標版本**下拉式清單，然後按一下左窗格中的 型別對應。  
  
## <a name="options"></a>選項。  
  
##### <a name="source-type"></a>來源類型  
它是具有要對應到目標資料庫的資料類型的 MySQL 資料型別。  
  
##### <a name="target-type"></a>目標類型  
目標資料庫資料類型指定的 MySQL 資料型別。  
  
##### <a name="add"></a>加入  
按一下以新增的資料類型對應清單。  
  
##### <a name="edit"></a>編輯  
按一下以編輯選取的資料類型對應清單中。  
  
##### <a name="remove"></a>移除  
按一下即可從對應清單中移除選取的資料類型對應。  
  
##### <a name="reset-to-default"></a>重設為預設值  
按一下 重設為 SSMA 預設值的類型對應清單。  
  
## <a name="type-mappings"></a>型別對應  
下表顯示來源和目標資料類型之間的預設對應  
  
|||  
|-|-|  
|**MySQL 資料類型**|**SQL Server 資料類型**|  
|bigint|bigint|  
|bigint [*..255]|bigint|  
|binary|二進位 [1]|  
|二進位 [0..1]|二進位 [1]|  
|二進位 [2..255]|二進位 [*]|  
|bit|二進位 [1]|  
|位元 [0..8]|二進位 [1]|  
|位元 [17..24]|二進位 [3]|  
|位元 [25..32]|二進位 [4]|  
|位元 [33..40]|二進位 [5]|  
|位元 [41..48]|二進位 [6]|  
|位元 [49..56]|二進位 [7]|  
|位元 [57..64]|二進位 [8]|  
|位元 [9..16]|二進位檔 [2]|  
|blob|varbinary(max)|  
|blob [0..1]|varbinary [1]|  
|blob [2..8000]|varbinary [*]|  
|blob [8001..*]|varbinary(max)|  
|bool|bit|  
|boolean|bit|  
|char|nchar [1]|  
|char 位元組|二進位 [1]|  
|char 位元組 [0..1]|二進位 [1]|  
|char 位元組 [2..255]|二進位 [*]|  
|char [0..1]|nchar [1]|  
|char [2..255]|nchar [*]|  
|character|nchar [1]|  
|字元不同 [0..1]|nvarchar [1]|  
|字元不同 [2..255]|nvarchar|  
|字元 [0..1]|nchar [1]|  
|字元 [2..255]|nchar [*]|  
|date|date|  
|datetime|datetime2 [0]|  
|dec|decimal|  
|dec [*..65]|decimal [*] [0]|  
|dec [*..65][\*..30]|decimal [*] [\*]|  
|decimal|decimal|  
|小數 [*..65]|decimal [*] [0]|  
|小數 [*..65][\*..30]|decimal [*] [\*]|  
|double|float [53]|  
|雙精度|float [53]|  
|雙精確度 [*..255][\*..30]|數字 [*][\*]|  
|double [*..255][\*..30]|數字 [*][\*]|  
|修正|numeric|  
|修正 [*..65][\*..30]|數字 [*][\*]|  
|float|float [24]|  
|float [*..255][\*..30]|數字 [*][\*]|  
|float [*..53]|float [53]|  
|int|int|  
|int [*..255]|int|  
|integer|int|  
|整數 [*..255]|int|  
|longblob|varbinary(max)|  
|長文字|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|int|  
|mediumint [*..255]|int|  
|mediumtext|nvarchar(max)|  
|國家 （地區) 的 char|nchar [1]|  
|國家 （地區) 的 char [0..1]|nchar [1]|  
|國家 （地區) 的 char [2..255]|nchar [*]|  
|國家字元集|nchar [1]|  
|不同的國家字元集|nvarchar [1]|  
|國家字元集變動 [0..1]|nvarchar [1]|  
|國家字元集變動 [2..4000]|nvarchar [*]|  
|不同的國家字元集 [4001..*]|nvarchar(max)|  
|國家字元集 [0..1]|nchar [1]|  
|國家字元集 [2..255]|nchar [*]|  
|國家 （地區) 的 varchar|nvarchar [1]|  
|國家 （地區) 的 varchar [0..1]|nvarchar [1]|  
|國家 （地區) 的 varchar [2..4000]|nvarchar [*]|  
|國家 （地區) 的 varchar [4001..*]|nvarchar(max)|  
|nchar|nchar [1]|  
|nchar varchar|nvarchar [1]|  
|nchar varchar [0..1]|nvarchar [1]|  
|nchar varchar [2..4000]|nvarchar [*]|  
|nchar varchar [4001..*]|nvarchar(max)|  
|nchar [0..1]|nchar [1]|  
|nchar [2..255]|nchar [*]|  
|numeric|numeric|  
|數字 [*..65]|數字 [*] [0]|  
|數字 [*..65][\*..30]|數字 [*][\*]|  
|nvarchar|nvarchar [1]|  
|nvarchar [0..1]|nvarchar [1]|  
|nvarchar [2..4000]|nvarchar [*]|  
|nvarchar [4001..*]|nvarchar(max)|  
|real|float [53]|  
|實際 [*..255][\*..30]|數字 [*][\*]|  
|序列|bigint|  
|smallint|smallint|  
|smallint [*..255]|smallint|  
|text|nvarchar(max)|  
|文字 [0..1]|nvarchar [1]|  
|文字 [2..4000]|nvarchar [*]|  
|文字 [4001..*]|nvarchar(max)|  
|time|time|  
|timestamp|datetime|  
|tinyblob|varbinary [255]|  
|tinyint|smallint|  
|tinyint [*..255]|smallint|  
|tinytext|nvarchar [255]|  
|不帶正負號的 bigint|bigint|  
|不帶正負號的 bigint [*..255]|bigint|  
|不帶正負號的 12 月|decimal|  
|不帶正負號的 dec [*..65]|decimal [*] [0]|  
|不帶正負號的 dec [*..65][\*..30]|decimal [*] [\*]|  
|不帶正負號的十進位|decimal|  
|不帶正負號的十進位 [*..65]|decimal [*] [0]|  
|不帶正負號的十進位 [*..65][\*..30]|decimal [*] [\*]|  
|不帶正負號的雙|float [53]|  
|不帶正負號的雙精度|float [53]|  
|不帶正負號雙精確度 [*..255][\*..30]|數字 [*][\*]|  
|不帶正負號 double [*..255][\*..30]|數字 [*][\*]|  
|不帶正負號固定|numeric|  
|不帶正負號固定 [*..65][\*..30]|數字 [*][\*]|  
|不帶正負號的浮點數|float [24]|  
|不帶正負號的浮點數 [*..255][\*..30]|數字 [*][\*]|  
|不帶正負號的浮點數 [*..53]|float [53]|  
|不帶正負號的整數|bigint|  
|不帶正負號的 int [*..255]|bigint|  
|不帶正負號的整數|bigint|  
|不帶正負號的整數 [*..255]|bigint|  
|不帶正負號的 mediumint|int|  
|不帶正負號的 mediumint [*..255]|int|  
|不帶正負號的數字|numeric|  
|不帶正負號的數字 [*..65]|數字 [*] [0]|  
|不帶正負號的數字 [*..65][\*..30]|數字 [*][\*]|  
|未簽署的真實|float [53]|  
|未簽署的真實 [*..255[[\*..30]|數字 [*][\*]|  
|不帶正負號的 smallint|int|  
|不帶正負號的 smallint [*..255]|int|  
|不帶正負號的 tinyint|tinyint|  
|不帶正負號的 tinyint [*..255]|tinyint|  
|varbinary [0..1]|varbinary [1]|  
|varbinary [2..8000]|varbinary [*]|  
|varbinary [8001..*]|varbinary(max)|  
|varchar [0..1]|nvarchar [1]|  
|varchar [2..4000]|nvarchar [*]|  
|varchar [4001..*]|nvarchar(max)|  
|year|smallint|  
|年 [2..2]|smallint|  
|年 [4..4]|smallint|  
  
##### <a name="add"></a>加入  
按一下以新增的資料類型對應清單。  
  
##### <a name="edit"></a>編輯  
按一下以編輯對應清單中的資料類型。  
  
##### <a name="remove"></a>移除  
按一下即可從對應清單中移除選取的資料類型對應。  
  
##### <a name="reset-to-default"></a>重設為預設值  
按一下以重設 SSMA 的所有資料類型對應。  
  
