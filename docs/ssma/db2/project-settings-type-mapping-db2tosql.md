---
title: 專案設定 （型別對應） (DB2ToSQL) |Microsoft 文件
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
ms.assetid: cf426c69-6a8e-4d19-951d-6661d5ae2562
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8232193c56feb0a9403b9cebaad896c7dbef8ad9
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34775284"
---
# <a name="project-settings-type-mapping-db2tosql"></a>專案設定 （型別對應） (DB2ToSQL)
類型對應 頁面**專案設定**對話方塊包含自訂 SSMA 如何轉換成的 DB2 資料類型的設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
型別對應的頁面位於**專案設定**和**預設專案設定**對話方塊。  
  
-   設定為所有未來的 SSMA 專案，指定上**工具**功能表上，按一下**預設專案設定**，選取移轉專案類型，不需要檢視或變更設定**移轉的目標版本**下拉式清單，然後按一下 **類型對應**在左窗格底部。  
  
-   若要指定目前的專案中，設定**工具**功能表上，按一下**專案設定**，然後按一下 **類型對應**在左窗格底部。  
  
若要指定目前的物件或物件類別的設定，請使用**類型對應**主要 SSMA 視窗索引標籤中的。  
  
## <a name="options"></a>選項。  
下表顯示**類型對應**索引標籤上選項：  
  
**來源類型**  
對應的 DB2 資料類型。  
  
**目標類型**  
目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]指定 DB2 資料類型的資料型別。  
  
請參閱下一節的 DB2 類型對應的預設值 SSMA 資料表。  
  
**[加入]**  
按一下以新增的資料類型對應清單。  
  
**編輯**  
按一下以編輯選取的資料類型對應清單中。  
  
**移除**  
按一下即可從對應清單中移除選取的資料類型對應。  
  
**重設預設值**  
按一下 重設為 SSMA 預設值的類型對應清單。  
  
## <a name="default-type-mappings"></a>預設型別對應  
SSMA for DB2，在您可以設定引數、 資料行、 區域變數和傳回值的自訂類型對應。 引數和傳回類型的預設對應是幾乎完全相同。  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>預設引數類型和傳回值類型對應  
下表包含引數和傳回值的預設資料類型對應。  
  
|DB2 資料類型|預設[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料類型|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_integer|ssNoversion|  
|blob|varbinary(max)|  
|boolean|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|Clob|varchar(max)|  
|日期|datetime2[0]|  
|dec|dec[38][0]|  
|Decimal|float [53]|  
|雙精度|float [53]|  
|FLOAT|float [53]|  
|ssNoversion|ssNoversion|  
|integer|ssNoversion|  
|long|varchar(max)|  
|長資料列|varbinary(max)|  
|長資料列 [\*..8000]<sup>*</sup>|varbinary[*]|  
|長資料列 [8001..\*]<sup>*</sup>|varbinary(max)|  
|國家 （地區) 的 char|nvarchar(max)|  
|不同國家 （地區) 的 char|nvarchar(max)|  
|國家字元集|nvarchar(max)|  
|不同的國家字元集<sup>**</sup>|nvarchar(max)|  
|不同的國家字元集<sup>*</sup>|nvarchar(max)|  
|NCHAR|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|number|float [53]|  
|NUMERIC|float [53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|ssNoversion|  
|未經處理的|varbinary(max)|  
|REAL|float [53]|  
|Rowid|UNIQUEIDENTIFIER|  
|Signtype|SMALLINT|  
|SMALLINT|SMALLINT|  
|string|varchar(max)|  
|TIMESTAMP|datetime2|  
|使用本地時區的時間戳記|datetimeoffset|  
|時區的時間戳記|datetimeoffset|  
|Urowid|UNIQUEIDENTIFIER|  
|varchar|varchar(max)|  
|varchar2|varchar(max)|  
|xmltype|xml|  
  
<sup>*</sup> 傳回值類型對應只會套用。  
  
<sup>**</sup> 引數型別對應只會套用。  
  
### <a name="default-column-type-mapping"></a>預設資料行型別對應  
下表包含資料行的預設型別對應。  
  
|DB2 資料類型|預設[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料類型|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|blob|varbinary(max)|  
|char|char|  
|char varying [*..\*]|varchar[*]|  
|char [*..\*]|char[*]|  
|character|char|  
|可變長度字元 [*..\*]|varchar[*]|  
|字元 [*..\*]|char[*]|  
|Clob|varchar(max)|  
|日期|datetime2[0]|  
|dec|dec[38][0]|  
|dec [*..\*]|dec[*][0]|  
|dec [*..\*][\*..\*]|dec[*][\*]|  
|Decimal|decimal[38][0]|  
|小數 [*..\*]|decimal[*][0]|  
|小數 [*..\*][\*..\*]|decimal[*][\*]|  
|雙精度|float [53]|  
|FLOAT|float [53]|  
|float [*..53]|float[*]|  
|float[54..*]|float [53]|  
|ssNoversion|ssNoversion|  
|integer|ssNoversion|  
|long|varchar(max)|  
|長資料列|varbinary(max)|  
|長資料列 [*..8000]|varbinary[*]|  
|長資料列 [8001..*]|varbinary(max)|  
|long varchar|varchar(max)|  
|長度 [*..8000]|varchar[*]|  
|long[8001..*]|varchar(max)|  
|國家 （地區) 的 char|NCHAR|  
|不同國家 （地區) 的 char [*..\*]|nvarchar[*]|  
|國家 （地區) 的 char [*..\*]|nchar[*]|  
|國家字元集|NCHAR|  
|不同的國家字元集 [*..\*]|nvarchar[*]|  
|國家字元集 [*..\*]|nchar[*]|  
|NCHAR|NCHAR|  
|nchar[*]|nchar[*]|  
|Nclob|nvarchar(max)|  
|number|float [53]|  
|數字 [*..\*]|numeric[*]|  
|數字 [*..\*][\*..\*]|數字 [*][\*]|  
|NUMERIC|NUMERIC|  
|數字 [*..\*]|numeric[*]|  
|數字 [*..\*][\*..\*]|數字 [*][\*]|  
|nvarchar2 [*..\*]|nvarchar[*]|  
|原始 [*..\*]|varbinary[*]|  
|REAL|float [53]|  
|Rowid|UNIQUEIDENTIFIER|  
|SMALLINT|SMALLINT|  
|TIMESTAMP|datetime2|  
|使用本地時區的時間戳記|datetimeoffset|  
|使用本地時區的時間戳記 [*..\*]|datetimeoffset[*]|  
|時區的時間戳記|datetimeoffset|  
|時區的時間戳記 [*..\*]|datetimeoffset[*]|  
|時間戳記 [*..\*]|datetime2[*]|  
|Urowid|UNIQUEIDENTIFIER|  
|urowid [*..\*]|UNIQUEIDENTIFIER|  
|varchar [*..\*]|varchar[*]|  
|varchar2 [*..\*]|varchar[*]|  
|Xmltype|xml|  
  
### <a name="default-local-variable-type-mapping"></a>預設本機變數的型別對應  
下表包含本機變數的預設型別對應。  
  
|DB2 資料類型|預設[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料類型|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_interger|ssNoversion|  
|Blob|varbinary(max)|  
|布林|bit|  
|Char|char|  
|char varying [*..8000]|varchar[*]|  
|char varying [8001..*]|varchar(max)|  
|char [*..8000]|char[*]|  
|char[8001..*]|varchar(max)|  
|字元|char|  
|可變長度字元 [*..8000]|varchar[*]|  
|可變長度字元 [8001..*]|varchar(max)|  
|字元 [*..8000]|char[*]|  
|character[8001..*]|varchar(max)|  
|Clob|varchar(max)|  
|日期|datetime2[0]|  
|dec|dec[38][0]|  
|dec [*..\*]|dec[*][0]|  
|dec [*..\*][\*..\*]|dec[*][\*]|  
|Decimal|decimal[38][0]|  
|小數 [*..\*]|decimal[*][0]|  
|小數 [*..\*][\*..\*]|decimal[*][\*]|  
|雙精度|float [53]|  
|float|float [53]|  
|float [*..53]|float[*]|  
|float[54..*]|float [53]|  
|int|ssNoversion|  
|Integer|ssNoversion|  
|整數 [*..\*]|numeric[*][0]|  
|長整數|varchar(max)|  
|長資料列|varbinary(max)|  
|長資料列 [*..8000]|varbinary[*]|  
|長資料列 [8001..*]|varbinary(max)|  
|國家 （地區) 的 char|NCHAR|  
|不同國家 （地區) 的 char [*..4000]|nvarchar[*]|  
|不同國家 （地區) 的 char [4001..*]|nvarchar(max)|  
|國家 （地區) 的 char [*..4000]|nchar[*]|  
|國家 （地區) 的 char [4001..*]|nvarchar(max)|  
|國家字元集|NCHAR|  
|國家字元集 [*..4000]|nvarchar[*]|  
|國家字元集 [4001..*]|nvarchar(max)|  
|不同的國家字元集 [*..4000]|nvarchar[*]|  
|不同的國家字元集 [4001..*]|nvarchar(max)|  
|Nchar|NCHAR|  
|nchar [*..4000]|nchar[*]|  
|nchar[4001..*]|nvarchar(max)|  
|nchar 變動 [*..4000]|nvarchar[*]|  
|nchar 變動 [4001..*]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|Number|float [53]|  
|數字 [*..\*]|numeric[*]|  
|數字 [*..\*][\*..\*]|數字 [*][\*]|  
|數值|numeric[38][0]|  
|數字 [*..\*]|numeric[*]|  
|數字 [*..\*][\*..\*]|數字 [*][\*]|  
|nvarchar2 [*..4000]|nvarchar[*]|  
|nvarchar2[4001..*]|nvarchar(max)|  
|pls_integer|ssNoversion|  
|原始 [*..8000]|varbinary[*]|  
|raw[8001..*]|varbinary(max)|  
|Real|float [53]|  
|Rowid|UNIQUEIDENTIFIER|  
|Signtype|SMALLINT|  
|Smallint|SMALLINT|  
|字串 [*..8000]|varchar[*]|  
|string[8001..*]|varchar(max)|  
|TIMESTAMP|datetime2|  
|使用本地時區的時間戳記|datetimeoffset|  
|時區的時間戳記|datetimeoffset|  
|使用本地時區的時間戳記 [*..\*]|datetimeoffset[*]|  
|時區的時間戳記 [*..\*]|datetimeoffset[*]|  
|時間戳記 [*..\*]|datetime2[*]|  
|Urowid|UNIQUEIDENTIFIER|  
|urowid [*..\*]|UNIQUEIDENTIFIER|  
|varchar [*..8000]|varchar[*]|  
|varchar[8001..*]|varchar(max)|  
|varchar2 [*..8000]|varchar[*]|  
|varchar2[8001..*]|varcha(max)|  
|Xmltype|xml|  
  
## <a name="see-also"></a>另請參閱  
[使用者介面參考&#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
