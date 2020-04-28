---
title: 專案設定（類型對應）（DB2ToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: cf426c69-6a8e-4d19-951d-6661d5ae2562
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7c0866a753bb61cb688ffe491e1de77431ddcb22
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68060166"
---
# <a name="project-settings-type-mapping-db2tosql"></a>專案設定（類型對應）（DB2ToSQL）
[**專案設定**] 對話方塊的 [類型對應] 頁面包含自訂 SSMA 如何將 DB2 資料類型轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成資料類型的設定。  
  
[類型對應] 頁面可在 [**專案設定**] 和 [**預設專案設定**] 對話方塊中取得。  
  
-   若要指定所有未來 SSMA 專案的設定，請在 [**工具**] 功能表上，按一下 [**預設專案設定**]，從 [**遷移目標版本**] 下拉式下選取需要查看或變更設定的 [遷移專案類型]，然後按一下左窗格底部的 [**類型對應**]。  
  
-   若要指定目前專案的設定，請在 [**工具**] 功能表上按一下 [**專案設定**]，然後按一下左窗格底部的 [**類型對應**]。  
  
若要指定目前物件或物件類別的設定，請使用主要 SSMA 視窗中的 [**類型對應**] 索引標籤。  
  
## <a name="options"></a>選項  
下表顯示 [**類型對應**] 索引標籤選項：  
  
**來源類型**  
對應的 DB2 資料類型。  
  
**目標型別**  
指定之[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB2 資料類型的目標資料類型。  
  
如需 DB2 型別對應的預設 SSMA，請參閱下一節中的表格。  
  
**加入**  
按一下即可將資料類型加入至 [對應] 清單。  
  
**編輯**  
按一下即可編輯 [對應] 清單中選取的資料類型。  
  
**移除**  
按一下即可從 [對應] 清單中移除選取的資料類型對應。  
  
**重設為預設值**  
按一下即可將 [類型對應] 清單重設為 SSMA 預設值。  
  
## <a name="default-type-mappings"></a>預設型別對應  
在 SSMA for DB2 中，您可以設定引數、資料行、區域變數和傳回值的自訂類型對應。 引數和傳回類型的預設對應幾乎完全相同。  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>預設引數型別和傳回值型別對應  
下表包含引數和傳回值的預設資料類型對應。  
  
|DB2 資料類型|預設[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型|  
|-----------------|-------------------------------------------------------------------------|  
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
|clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|decimal|float [53]|  
|雙精度|float [53]|  
|FLOAT|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|長原始|varbinary(max)|  
|長時間原始\*[.。8000]<sup>\*</sup>|Varbinary [\*]|  
|冗長的原始 [8001 ...\*]<sup>\*</sup>|varbinary(max)|  
|國家/地區|nvarchar(max)|  
|國家/地區 char 改變|nvarchar(max)|  
|國家字元|nvarchar(max)|  
|國家字元變動<sup>\*\*</sup>|nvarchar(max)|  
|國家字元變動<sup>\*</sup>|nvarchar(max)|  
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
|具有當地時區的時間戳記|datetimeoffset|  
|含時區的時間戳記|datetimeoffset|  
|urowid|UNIQUEIDENTIFIER|  
|varchar|varchar(max)|  
|Varchar2|varchar(max)|  
|xmltype|Xml|  
  
<sup>\*</sup>僅適用于傳回值型別對應。  
  
<sup>\*\*</sup>僅適用于引數類型對應。  
  
### <a name="default-column-type-mapping"></a>預設資料行類型對應  
下表包含資料行的預設類型對應。  
  
|DB2 資料類型|預設[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型|  
|-----------------|-------------------------------------------------------------------------|  
|bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|blob|varbinary(max)|  
|char|char|  
|char 改變 [\*.。\*]|Varchar [\*]|  
|char [\*.。\*]|char [\*]|  
|character|char|  
|字元變動 [\*.。\*]|Varchar [\*]|  
|字元 [\*.。\*]|char [\*]|  
|clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|dec [\*.。\*]|dec [\*] [0]|  
|dec [\*.。\*][\*..\*]|dec [\*] [\*]|  
|decimal|decimal [38] [0]|  
|decimal [\*.。\*]|decimal [\*] [0]|  
|decimal [\*.。\*][\*..\*]|decimal [\*] [\*]|  
|雙精度|float [53]|  
|FLOAT|float [53]|  
|float [\*.。53]|float [\*]|  
|float [54..\*]|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|長原始|varbinary(max)|  
|長時間原始\*[.。8000]|Varbinary [\*]|  
|冗長的原始 [8001 ...\*]|varbinary(max)|  
|長 varchar|varchar(max)|  
|long [\*.。8000]|Varchar [\*]|  
|long [8001 ...\*]|varchar(max)|  
|國家/地區|NCHAR|  
|國家 char 改變 [\*.。\*]|Nvarchar [\*]|  
|國家 char [\*.。\*]|Nchar [\*]|  
|國家字元|NCHAR|  
|國家字元變動 [\*.。\*]|Nvarchar [\*]|  
|國家字元 [\*.。\*]|Nchar [\*]|  
|NCHAR|NCHAR|  
|Nchar [\*]|Nchar [\*]|  
|nclob|nvarchar(max)|  
|number|float [53]|  
|數位 [\*.。\*]|數值 [\*]|  
|數位 [\*.。\*][\*..\*]|數值 [\*] [\*]|  
|NUMERIC|NUMERIC|  
|數值 [\*.。\*]|數值 [\*]|  
|數值 [\*.。\*][\*..\*]|數值 [\*] [\*]|  
|Nvarchar2 [\*.。。\*]|Nvarchar [\*]|  
|原始 [\*.。\*]|Varbinary [\*]|  
|real|float [53]|  
|rowid|UNIQUEIDENTIFIER|  
|SMALLINT|SMALLINT|  
|timestamp|datetime2|  
|具有當地時區的時間戳記|datetimeoffset|  
|具有當地時區的時間戳記\*[.。\*]|datetimeoffset [\*]|  
|含時區的時間戳記|datetimeoffset|  
|具有時區的時間戳記\*[.。\*]|datetimeoffset [\*]|  
|時間戳記\*[.。\*]|datetime2 [\*]|  
|Urowid|UNIQUEIDENTIFIER|  
|urowid [\*.。。\*]|UNIQUEIDENTIFIER|  
|Varchar [\*.。\*]|Varchar [\*]|  
|Varchar2 [\*.。。\*]|Varchar [\*]|  
|Xmltype|Xml|  
  
### <a name="default-local-variable-type-mapping"></a>預設本機變數類型對應  
下表包含本機變數的預設型別對應。  
  
|DB2 資料類型|預設[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型|  
|-----------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_interger|int|  
|Blob|varbinary(max)|  
|Boolean|bit|  
|Char|char|  
|char 改變 [\*.。8000]|Varchar [\*]|  
|char 改變 [8001 ...\*]|varchar(max)|  
|char [\*.。8000]|char [\*]|  
|char [8001 ...\*]|varchar(max)|  
|字元|char|  
|字元變動 [\*.。8000]|Varchar [\*]|  
|字元變動 [8001 ...\*]|varchar(max)|  
|字元 [\*.。8000]|char [\*]|  
|字元 [8001 ...\*]|varchar(max)|  
|clob|varchar(max)|  
|date|datetime2 [0]|  
|dec|dec [38] [0]|  
|dec [\*.。\*]|dec [\*] [0]|  
|dec [\*.。\*][\*..\*]|dec [\*] [\*]|  
|decimal|decimal [38] [0]|  
|decimal [\*.。\*]|decimal [\*] [0]|  
|decimal [\*.。\*][\*..\*]|decimal [\*] [\*]|  
|雙精度|float [53]|  
|Float|float [53]|  
|float [\*.。53]|float [\*]|  
|float [54..\*]|float [53]|  
|Int|int|  
|整數|int|  
|整數 [\*.。\*]|數值 [\*] [0]|  
|long|varchar(max)|  
|長原始|varbinary(max)|  
|長時間原始\*[.。8000]|Varbinary [\*]|  
|冗長的原始 [8001 ...\*]|varbinary(max)|  
|國家/地區|NCHAR|  
|國家 char 改變 [\*.。4000]|Nvarchar [\*]|  
|國家/地區不同 [4001\*]|nvarchar(max)|  
|國家 char [\*.。4000]|Nchar [\*]|  
|國家字元 [4001 ...\*]|nvarchar(max)|  
|國家字元|NCHAR|  
|國家字元 [\*.。4000]|Nvarchar [\*]|  
|國家字元 [4001 ...\*]|nvarchar(max)|  
|國家字元變動 [\*.。4000]|Nvarchar [\*]|  
|國家字元變動 [4001 ...\*]|nvarchar(max)|  
|Nchar|NCHAR|  
|Nchar [\*.。4000]|Nchar [\*]|  
|Nchar [4001 ...\*]|nvarchar(max)|  
|Nchar 改變 [\*.。4000]|Nvarchar [\*]|  
|Nchar 改變 [4001 ...\*]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|Number|float [53]|  
|數位 [\*.。\*]|數值 [\*]|  
|數位 [\*.。\*][\*..\*]|數值 [\*] [\*]|  
|數值|數值 [38] [0]|  
|數值 [\*.。\*]|數值 [\*]|  
|數值 [\*.。\*][\*..\*]|數值 [\*] [\*]|  
|Nvarchar2 [\*.。。4000]|Nvarchar [\*]|  
|Nvarchar2 [4001 ...\*]|nvarchar(max)|  
|pls_integer|int|  
|原始 [\*.。8000]|Varbinary [\*]|  
|原始 [8001 ...\*]|varbinary(max)|  
|Real|float [53]|  
|Rowid|UNIQUEIDENTIFIER|  
|Signtype|SMALLINT|  
|Smallint|SMALLINT|  
|字串 [\*.。8000]|Varchar [\*]|  
|string [8001 ...\*]|varchar(max)|  
|timestamp|datetime2|  
|具有當地時區的時間戳記|datetimeoffset|  
|含時區的時間戳記|datetimeoffset|  
|具有當地時區的時間戳記\*[.。\*]|datetimeoffset [\*]|  
|具有時區的時間戳記\*[.。\*]|datetimeoffset [\*]|  
|時間戳記\*[.。\*]|datetime2 [\*]|  
|Urowid|UNIQUEIDENTIFIER|  
|urowid [\*.。。\*]|UNIQUEIDENTIFIER|  
|Varchar [\*.。8000]|Varchar [\*]|  
|Varchar [8001 ...\*]|varchar(max)|  
|Varchar2 [\*.。。8000]|Varchar [\*]|  
|Varchar2 [8001\*]|varcha （max）|  
|Xmltype|Xml|  
  
## <a name="see-also"></a>另請參閱  
[&#40;DB2ToSQL&#41;的使用者介面參考](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
