---
description: 專案設定 (類型對應) (OracleToSQL)
title: 專案設定 (類型對應)  (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4bb8466e-2199-4f00-8513-b04e9586723d
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 0facd2ecca0ff6cc0a4bc28fe709a7adfc0c5acf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88320444"
---
# <a name="project-settings-type-mapping-oracletosql"></a>專案設定 (類型對應) (OracleToSQL)
[ **專案設定** ] 對話方塊的 [類型對應] 頁面包含設定，這些設定會自訂 SSMA 將 Oracle 資料類型轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的方式。  
  
[類型對應] 頁面可在 [ **專案設定** ] 和 [ **預設專案設定** ] 對話方塊中使用。  
  
-   若要指定所有未來 SSMA 專案的設定，請在 [ **工具** ] 功能表上按一下 [ **預設專案設定**]，選取 [遷移專案類型]，需要從 [ **遷移目標版本** ] 下拉式清單中查看或變更設定，然後按一下左窗格底部的 [ **類型對應** ]。  
  
-   若要指定目前專案的設定，請按一下 [ **工具** ] 功能表上的 [ **專案設定**]，然後按一下左窗格底部的 [ **類型對應** ]。  
  
若要指定物件的目前物件或類別的設定，請使用主要 SSMA 視窗中的 [ **類型對應** ] 索引標籤。  
  
## <a name="options"></a>選項。  
下表顯示 [ **類型對應** ] 索引標籤選項：  
  
**來源類型**  
對應的 Oracle 資料類型。  
  
**目標型別**  
指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle 資料類型的目標資料類型。  
  
如需 Oracle 類型對應的預設 SSMA，請參閱下一節中的表格。  
  
**加入**  
按一下以將資料類型加入至對應清單。  
  
**編輯**  
按一下即可編輯 [對應] 清單中所選取的資料類型。  
  
**移除**  
按一下即可從 [對應] 清單中移除選取的資料類型對應。  
  
**重設為預設值**  
按一下以將類型對應清單重設為 SSMA 預設值。  
  
## <a name="default-type-mappings"></a>預設型別對應  
在 SSMA for Oracle 中，您可以為引數、資料行、區域變數和傳回值設定自訂類型對應。 引數和傳回類型的預設對應幾乎完全相同。  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>預設引數型別和傳回值型別對應  
下表包含引數和傳回值的預設資料類型對應。  
  
|Oracle 資料類型|預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型|  
|--------------------|-------------------------------------------------------------------------|  
|bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_integer|int|  
|blob|varbinary(max)|  
|boolean|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|Clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|decimal|float [53]|  
|雙精度|float [53]|  
|FLOAT|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|long raw|varbinary(max)|  
|long raw [ \* .。。8000]<sup>*</sup>|Varbinary [*]|  
|long raw [8001 ... \* ]<sup>*</sup>|varbinary(max)|  
|國家/地區字元|nvarchar(max)|  
|國家字元變動|nvarchar(max)|  
|國家字元|nvarchar(max)|  
|國家字元變動<sup>**</sup>|nvarchar(max)|  
|國家字元變動<sup>*</sup>|nvarchar(max)|  
|NCHAR|nvarchar(max)|  
|nclob|nvarchar(max)|  
|number|float [53]|  
|NUMERIC|float [53]|  
|Nvarchar2|nvarchar(max)|  
|pls_integer|int|  
|raw|varbinary(max)|  
|real|float [53]|  
|rowid|UNIQUEIDENTIFIER|  
|signtype|SMALLINT|  
|SMALLINT|SMALLINT|  
|字串|varchar(max)|  
|timestamp|datetime2|  
|具有本地時區的時間戳記|datetimeoffset|  
|具有時區的時間戳記|datetimeoffset|  
|urowid|UNIQUEIDENTIFIER|  
|varchar|varchar(max)|  
|Varchar2|varchar(max)|  
|xmltype|Xml|  
  
<sup>*</sup> 只適用于傳回值型別對應。  
  
<sup>**</sup> 只適用于引數型別對應。  
  
### <a name="default-column-type-mapping"></a>預設資料行類型對應  
下表包含資料行的預設型別對應。  
  
|Oracle 資料類型|預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型|  
|--------------------|-------------------------------------------------------------------------|  
|bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|blob|varbinary(max)|  
|char|char|  
|char 變化 [* ... \* ]|Varchar [*]|  
|char [* ... \* ]|char [*]|  
|character|char|  
|字元差異 [* ... \* ]|Varchar [*]|  
|字元 [* ... \* ]|char [*]|  
|Clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|dec [* ... \* ]|dec [*] [0]|  
|dec [* ... \* ][\*..\*]|dec [*] [ \* ]|  
|decimal|decimal [38] [0]|  
|decimal [* ... \* ]|decimal [*] [0]|  
|decimal [* ... \* ][\*..\*]|decimal [*] [ \* ]|  
|雙精度|float [53]|  
|FLOAT|float [53]|  
|float [* .。。53]|float [*]|  
|float [54.. *]|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|long raw|varbinary(max)|  
|long raw [* .。。8000]|Varbinary [*]|  
|long raw [8001 ... *]|varbinary(max)|  
|長 varchar|varchar(max)|  
|long [*.。8000]|Varchar [*]|  
|long [8001 ... *]|varchar(max)|  
|國家/地區字元|NCHAR|  
|國家 char 變化 [* ... \* ]|Nvarchar [*]|  
|國家字元 [* ... \* ]|Nchar [*]|  
|國家字元|NCHAR|  
|國際字元不同 [* ... \* ]|Nvarchar [*]|  
|國家字元 [* ... \* ]|Nchar [*]|  
|NCHAR|NCHAR|  
|Nchar [*]|Nchar [*]|  
|nclob|nvarchar(max)|  
|number|float [53]|  
|數位 [* ... \* ]|數值 [*]|  
|數位 [* ... \* ][\*..\*]|數值 [*] [ \* ]|  
|NUMERIC|NUMERIC|  
|數值 [* ... \* ]|數值 [*]|  
|數值 [* ... \* ][\*..\*]|數值 [*] [ \* ]|  
|Nvarchar2 [* ... \* ]|Nvarchar [*]|  
|raw [* ... \* ]|Varbinary [*]|  
|real|float [53]|  
|rowid|UNIQUEIDENTIFIER|  
|SMALLINT|SMALLINT|  
|timestamp|datetime2|  
|具有本地時區的時間戳記|datetimeoffset|  
|具有本地時區的時間戳記 [* ... \* ]|datetimeoffset [*]|  
|具有時區的時間戳記|datetimeoffset|  
|具有時區的時間戳記 [* ... \* ]|datetimeoffset [*]|  
|timestamp [* ... \* ]|datetime2 [*]|  
|Urowid|UNIQUEIDENTIFIER|  
|urowid [* ... \* ]|UNIQUEIDENTIFIER|  
|Varchar [* ... \* ]|Varchar [*]|  
|Varchar2 [* ... \* ]|Varchar [*]|  
|Xmltype|Xml|  
  
### <a name="default-local-variable-type-mapping"></a>預設本機變數型別對應  
下表包含本機變數的預設型別對應。  
  
|Oracle 資料類型|預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型|  
|--------------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_interger|int|  
|Blob|varbinary(max)|  
|布林值|bit|  
|Char|char|  
|char 改變 [*.。8000]|Varchar [*]|  
|char 變化 [8001 ... *]|varchar(max)|  
|char [* .。。8000]|char [*]|  
|char [8001 ... *]|varchar(max)|  
|字元|char|  
|字元差異 [* .。。8000]|Varchar [*]|  
|字元差異 [8001 ... *]|varchar(max)|  
|字元 [* .。。8000]|char [*]|  
|字元 [8001 ... *]|varchar(max)|  
|Clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|dec [* ... \* ]|dec [*] [0]|  
|dec [* ... \* ][\*..\*]|dec [*] [ \* ]|  
|decimal|decimal [38] [0]|  
|decimal [* ... \* ]|decimal [*] [0]|  
|decimal [* ... \* ][\*..\*]|decimal [*] [ \* ]|  
|雙精度|float [53]|  
|Float|float [53]|  
|float [* .。。53]|float [*]|  
|float [54.. *]|float [53]|  
|Int|int|  
|整數|int|  
|整數 [* ... \* ]|數值 [*] [0]|  
|long|varchar(max)|  
|long raw|varbinary(max)|  
|long raw [* .。。8000]|Varbinary [*]|  
|long raw [8001 ... *]|varbinary(max)|  
|國家/地區字元|NCHAR|  
|國家字元變化 [*.。4000]|Nvarchar [*]|  
|國家字元變化 [4001.. *]|nvarchar(max)|  
|國家字元 [*.。4000]|Nchar [*]|  
|國家字元 [4001.. *]|nvarchar(max)|  
|國家字元|NCHAR|  
|國家字元 [*.。4000]|Nvarchar [*]|  
|國家字元 [4001.. *]|nvarchar(max)|  
|國際字元不同 [*.。4000]|Nvarchar [*]|  
|國際字元不同 [4001 ... *]|nvarchar(max)|  
|Nchar|NCHAR|  
|Nchar [* .。。4000]|Nchar [*]|  
|Nchar [4001.. *]|nvarchar(max)|  
|Nchar 不同 [*.。4000]|Nvarchar [*]|  
|Nchar 變化 [4001 ... *]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|Number|float [53]|  
|數位 [* ... \* ]|數值 [*]|  
|數位 [* ... \* ][\*..\*]|數值 [*] [ \* ]|  
|數值|數值 [38] [0]|  
|數值 [* ... \* ]|數值 [*]|  
|數值 [* ... \* ][\*..\*]|數值 [*] [ \* ]|  
|Nvarchar2 [* .。。4000]|Nvarchar [*]|  
|Nvarchar2 [4001.. *]|nvarchar(max)|  
|pls_integer|int|  
|raw [* .。。8000]|Varbinary [*]|  
|raw [8001 ... *]|varbinary(max)|  
|Real|float [53]|  
|Rowid|UNIQUEIDENTIFIER|  
|Signtype|SMALLINT|  
|Smallint|SMALLINT|  
|字串 [* .。。8000]|Varchar [*]|  
|字串 [8001 ... *]|varchar(max)|  
|timestamp|datetime2|  
|具有本地時區的時間戳記|datetimeoffset|  
|具有時區的時間戳記|datetimeoffset|  
|具有本地時區的時間戳記 [* ... \* ]|datetimeoffset [*]|  
|具有時區的時間戳記 [* ... \* ]|datetimeoffset [*]|  
|timestamp [* ... \* ]|datetime2 [*]|  
|Urowid|UNIQUEIDENTIFIER|  
|urowid [* ... \* ]|UNIQUEIDENTIFIER|  
|Varchar [* .。。8000]|Varchar [*]|  
|Varchar [8001 ... *]|varchar(max)|  
|Varchar2 [* .。。8000]|Varchar [*]|  
|Varchar2 [8001 ... *]|varcha (最大) |  
|Xmltype|Xml|  
  
## <a name="see-also"></a>另請參閱  
[消費者介面參考 &#40;OracleToSQL&#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
