---
description: 中繼資料-SQL Server Native Client 中的參數和資料列集
title: '參數和資料列集中繼資料 (Native Client OLE DB 提供者) '
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
ms.assetid: 31b318a4-20e7-4db0-b367-eb9938859029
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f45147881ec8cc2c62f8d023a1fe443164682678
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88381744"
---
# <a name="metadata---parameter-and-rowset-in-sql-server-native-client"></a>中繼資料-SQL Server Native Client 中的參數和資料列集
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  本主題提供有關下列與 OLE DB 日期和時間增強功能相關之類型和類型成員的資訊。  
  
-   DBBINDING 結構  
  
-   **ICommandWithParameters::GetParameterInfo**  
  
-   **ICommandWithParameters::SetParameterInfo**  
  
-   **IColumnsRowset::GetColumnsRowset**  
  
-   **IColumnsInfo::GetColumnInfo**  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 下列資訊會以 DBPARAMINFO 結構透過 *prgParamInfo* 傳回：  
  
|參數類型|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|-------------------|------------------|--------------|-----------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|Set|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19，21. 27|0..7|Set|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26，28. 34|0..7|Set|  
  
 請注意，在某些情況下值的範圍並不是連續的。 這是當小數有效位數大於零時增加的小數點所導致。  
  
 只有連接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (或更新版本) 伺服器時，DBPARAMFLAGS_SS_ISVARIABLESCALE 才有效。 連接到下層伺服器時，永遠不會設定 DBPARAMFLAGS_SS_ISVARIABLESCALE。  
  
## <a name="icommandwithparameterssetparameterinfo-and-implied-parameter-types"></a>ICommandWithParameters::SetParameterInfo 和隱含參數類型  
 以 DBPARAMBINDINFO 結構所提供的資訊必須與下列相符：  
  
|*pwszDataSourceType*<br /><br /> (提供者特定)|*pwszDataSourceType*<br /><br /> (OLE DB 一般)|*ulParamSize*|*bScale*|  
|----------------------------------------------------|-------------------------------------------------|-------------------|--------------|  
||DBTYPE_DATE|6|忽略|  
|date|DBTYPE_DBDATE|6|忽略|  
||DBTYPE_DBTIME|10|忽略|  
|time|DBTYPE_DBTIME2|10|0..7|  
|smalldatetime||16|忽略|  
|Datetime||16|忽略|  
|datetime2 或 DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|16|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|0..7|  
  
 已忽略 *bPrecision* 參數。  
  
 當傳送資料到伺服器時，"DBPARAMFLAGS_SS_ISVARIABLESCALE" 會被忽略。 應用程式可以使用提供者特定的類型名稱 "**datetime**" 和 "**smalldatetime**" 來強制使用舊版的表格式資料流 (TDS) 類型。 當連接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (或更新版本) 伺服器時，會使用 "**datetime2**" 格式，而且當類型名稱為 "**datetime2**" 或 "DBTYPE_DBTIMESTAMP" 時，會發生隱含的伺服器轉換 (如有必要)。 如果使用了提供者特定的類型名稱 "**datetime**" 或 "**smalldatetime**"，就會忽略 *bScale*。 否則，html5 應用程式必須確定已正確設定 *bScale* 。 從 MDAC 升級的應用程式和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 使用 "DBTYPE_DBTIMESTAMP" 的 Native Client，如果未正確設定 *bScale* ，則會失敗。 連接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前版本的伺服器執行個體時，*bScale* 值如果不是 0 或 3 且具有 "DBTYPE_DBTIMESTAMP"，便是錯誤且會傳回 E_FAIL。  
  
 未呼叫 ICommandWithParameters：： SetParameterInfo 時，提供者會依照 IAccessor：： CreateAccessor 中指定的系結類型來推斷伺服器類型，如下所示：  
  
|繫結類型|*pwszDataSourceType*<br /><br /> (提供者特定)|  
|------------------|----------------------------------------------------|  
|DBTYPE_DATE|datetime2(0)|  
|DBTYPE_DBDATE|date|  
|DBTYPE_DBTIME|time(0)|  
|DBTYPE_DBTIME2|time(7)|  
|DBTYPE_DBTIMESTAMP|datetime2(7)|  
|DBTYPE_DBTIMESTAMPOFFSET|datetimeoffset(7)|  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 **IColumnsRowset::GetColumnsRowset** 會傳回下列資料行：  
  
|資料行類型|DBCOLUMN_TYPE|DBCOLUM_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE、DBCOLUMN_DATETIMEPRECISION|DBCOLUMN_FLAGS, DBCOLUMNFLAGS_SS_ISVARIABLESCALE|  
|-----------------|--------------------|-------------------------|-------------------------|--------------------------------------------------|---------------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|Set|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Set|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Set|  
  
 在 DBCOLUMN_FLAGS 中，DBCOLUMNFLAGS_ISFIXEDLENGTH 對 date/time 類型永遠為 true，而且下列旗標永遠為 false：  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 剩餘的旗標 (DBCOLUMNFLAGS_ISNULLABLE、DBCOLUMNFLAGS_MAYBENULL、DBCOLUMNFLAGS_WRITE 和 DBCOLUMNFLAGS_WRITEUNKNOWN) 可以根據資料行的定義方式以及實際的查詢來設定。  
  
 在 DBCOLUMN_FLAGS 中會提供新旗標 DBCOLUMNFLAGS_SS_ISVARIABLESCALE，以允許應用程式判斷資料行的伺服器類型，其中 DBCOLUMN_TYPE 是 DBTYPE_DBTIMESTAMP。 DBCOLUMN_SCALE 或 DBCOLUMN_DATETIMEPRECISION 也必須用來識別伺服器類型。  
  
 只有連接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (或更新版本) 伺服器時，DBCOLUMNFLAGS_SS_ISVARIABLESCALE 才有效。 連接到下層伺服器時，不會定義 DBCOLUMNFLAGS_SS_ISVARIABLESCALE。  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 結構會傳回下列資訊：  
  
|參數類型|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Clear|  
|time(1..7)|DBTYPE_DBTIME2|10|8, 10..16|0..7|Set|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Set|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Set|  
  
 在 *dwFlags* 中，DBCOLUMNFLAGS_ISFIXEDLENGTH 對 date/time 類型永遠為 true，而且下列旗標永遠為 false：  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER, MAYDEFER  
  
 可以設定剩餘的旗標 (DBCOLUMNFLAGS_ISNULLABLE、DBCOLUMNFLAGS_MAYBENULL、DBCOLUMNFLAGS_WRITE 和 DBCOLUMNFLAGS_WRITEUNKNOWN)。  
  
 在 *dwFlags* 中會提供新旗標 DBCOLUMNFLAGS_SS_ISVARIABLESCALE，以允許應用程式判斷資料行的伺服器類型，其中 *wType* 是 DBTYPE_DBTIMESTAMP。 *bScale* 也必須用來識別伺服器類型。  
  
## <a name="see-also"></a>另請參閱  
 [中繼資料 &#40;OLE DB&#41;](https://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
  
  
