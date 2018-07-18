---
title: 專案設定 （型別對應） (MySQLToSQL) |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 136fdf6d-657f-447b-af41-49bbc6e0e93e
caps.latest.revision: 13
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9bf1d1c219b8673345d5f2074fe8885b5c58223f
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776763"
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
|BIGINT|BIGINT|  
|bigint [*..255]|BIGINT|  
|BINARY|二進位 [1]|  
|binary[0..1]|二進位 [1]|  
|binary[2..255]|binary[*]|  
|bit|二進位 [1]|  
|bit[0..8]|二進位 [1]|  
|bit[17..24]|二進位 [3]|  
|bit[25..32]|二進位 [4]|  
|bit[33..40]|二進位 [5]|  
|bit[41..48]|二進位 [6]|  
|bit[49..56]|二進位 [7]|  
|bit[57..64]|二進位 [8]|  
|bit[9..16]|二進位檔 [2]|  
|blob|varbinary(max)|  
|blob[0..1]|varbinary [1]|  
|blob[2..8000]|varbinary[*]|  
|blob[8001..*]|varbinary(max)|  
|bool|bit|  
|boolean|bit|  
|char|nchar [1]|  
|char 位元組|二進位 [1]|  
|char 位元組 [0..1]|二進位 [1]|  
|char 位元組 [2..255]|binary[*]|  
|char[0..1]|nchar [1]|  
|char[2..255]|nchar[*]|  
|character|nchar [1]|  
|字元不同 [0..1]|nvarchar [1]|  
|字元不同 [2..255]|NVARCHAR|  
|character[0..1]|nchar [1]|  
|character[2..255]|nchar[*]|  
|日期|日期|  
|DATETIME|datetime2[0]|  
|dec|Decimal|  
|dec [*..65]|decimal[*][0]|  
|dec [*..65][\*..30]|decimal[*][\*]|  
|Decimal|Decimal|  
|小數 [*..65]|decimal[*][0]|  
|小數 [*..65][\*..30]|decimal[*][\*]|  
|double|float [53]|  
|雙精度|float [53]|  
|雙精確度 [*..255][\*..30]|數字 [*][\*]|  
|double [*..255][\*..30]|數字 [*][\*]|  
|修正|NUMERIC|  
|修正 [*..65][\*..30]|數字 [*][\*]|  
|FLOAT|float[24]|  
|float [*..255][\*..30]|數字 [*][\*]|  
|float [*..53]|float [53]|  
|ssNoversion|ssNoversion|  
|int [*..255]|ssNoversion|  
|integer|ssNoversion|  
|整數 [*..255]|ssNoversion|  
|longblob|varbinary(max)|  
|長文字|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|ssNoversion|  
|mediumint [*..255]|ssNoversion|  
|mediumtext|nvarchar(max)|  
|國家 （地區) 的 char|nchar [1]|  
|國家 （地區) 的 char [0..1]|nchar [1]|  
|國家 （地區) 的 char [2..255]|nchar[*]|  
|國家字元集|nchar [1]|  
|不同的國家字元集|nvarchar [1]|  
|國家字元集變動 [0..1]|nvarchar [1]|  
|國家字元集變動 [2..4000]|nvarchar[*]|  
|不同的國家字元集 [4001..*]|nvarchar(max)|  
|國家字元集 [0..1]|nchar [1]|  
|國家字元集 [2..255]|nchar[*]|  
|國家 （地區) 的 varchar|nvarchar [1]|  
|國家 （地區) 的 varchar [0..1]|nvarchar [1]|  
|國家 （地區) 的 varchar [2..4000]|nvarchar[*]|  
|國家 （地區) 的 varchar [4001..*]|nvarchar(max)|  
|NCHAR|nchar [1]|  
|nchar varchar|nvarchar [1]|  
|nchar varchar [0..1]|nvarchar [1]|  
|nchar varchar [2..4000]|nvarchar[*]|  
|nchar varchar [4001..*]|nvarchar(max)|  
|nchar[0..1]|nchar [1]|  
|nchar[2..255]|nchar[*]|  
|NUMERIC|NUMERIC|  
|數字 [*..65]|numeric[*][0]|  
|數字 [*..65][\*..30]|數字 [*][\*]|  
|NVARCHAR|nvarchar [1]|  
|nvarchar[0..1]|nvarchar [1]|  
|nvarchar[2..4000]|nvarchar[*]|  
|nvarchar[4001..*]|nvarchar(max)|  
|REAL|float [53]|  
|實際 [*..255][\*..30]|數字 [*][\*]|  
|序列|BIGINT|  
|SMALLINT|SMALLINT|  
|smallint [*..255]|SMALLINT|  
|text|nvarchar(max)|  
|text[0..1]|nvarchar [1]|  
|text[2..4000]|nvarchar[*]|  
|text[4001..*]|nvarchar(max)|  
|time|time|  
|TIMESTAMP|DATETIME|  
|tinyblob|varbinary [255]|  
|TINYINT|SMALLINT|  
|tinyint [*..255]|SMALLINT|  
|tinytext|nvarchar[255]|  
|不帶正負號的 bigint|BIGINT|  
|不帶正負號的 bigint [*..255]|BIGINT|  
|不帶正負號的 12 月|Decimal|  
|不帶正負號的 dec [*..65]|decimal[*][0]|  
|不帶正負號的 dec [*..65][\*..30]|decimal[*][\*]|  
|不帶正負號的十進位|Decimal|  
|不帶正負號的十進位 [*..65]|decimal[*][0]|  
|不帶正負號的十進位 [*..65][\*..30]|decimal[*][\*]|  
|不帶正負號的雙|float [53]|  
|不帶正負號的雙精度|float [53]|  
|不帶正負號雙精確度 [*..255][\*..30]|數字 [*][\*]|  
|不帶正負號 double [*..255][\*..30]|數字 [*][\*]|  
|不帶正負號固定|NUMERIC|  
|不帶正負號固定 [*..65][\*..30]|數字 [*][\*]|  
|不帶正負號的浮點數|float[24]|  
|不帶正負號的浮點數 [*..255][\*..30]|數字 [*][\*]|  
|不帶正負號的浮點數 [*..53]|float [53]|  
|不帶正負號的整數|BIGINT|  
|不帶正負號的 int [*..255]|BIGINT|  
|不帶正負號的整數|BIGINT|  
|不帶正負號的整數 [*..255]|BIGINT|  
|不帶正負號的 mediumint|ssNoversion|  
|不帶正負號的 mediumint [*..255]|ssNoversion|  
|不帶正負號的數字|NUMERIC|  
|不帶正負號的數字 [*..65]|numeric[*][0]|  
|不帶正負號的數字 [*..65][\*..30]|數字 [*][\*]|  
|未簽署的真實|float [53]|  
|未簽署的真實 [*..255[[\*..30]|數字 [*][\*]|  
|不帶正負號的 smallint|ssNoversion|  
|不帶正負號的 smallint [*..255]|ssNoversion|  
|不帶正負號的 tinyint|TINYINT|  
|不帶正負號的 tinyint [*..255]|TINYINT|  
|varbinary[0..1]|varbinary [1]|  
|varbinary[2..8000]|varbinary[*]|  
|varbinary[8001..*]|varbinary(max)|  
|varchar[0..1]|nvarchar [1]|  
|varchar[2..4000]|nvarchar[*]|  
|varchar[4001..*]|nvarchar(max)|  
|year|SMALLINT|  
|year[2..2]|SMALLINT|  
|year[4..4]|SMALLINT|  
  
##### <a name="add"></a>加入  
按一下以新增的資料類型對應清單。  
  
##### <a name="edit"></a>編輯  
按一下以編輯對應清單中的資料類型。  
  
##### <a name="remove"></a>移除  
按一下即可從對應清單中移除選取的資料類型對應。  
  
##### <a name="reset-to-default"></a>重設為預設值  
按一下以重設 SSMA 的所有資料類型對應。  
  
