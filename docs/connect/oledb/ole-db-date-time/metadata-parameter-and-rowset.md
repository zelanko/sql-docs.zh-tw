---
title: 參數和資料列集中繼資料 | Microsoft Docs
description: 參數和資料列集的中繼資料
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 641859e134a5f3c3201f239023f911b79de1c11e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67995093"
---
# <a name="metadata---parameter-and-rowset"></a>中繼資料 - 參數和資料列集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本文提供有關下列與 OLE DB 日期和時間增強功能相關之類型和類型成員的資訊。  
  
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
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|設定|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|設定|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|設定|  
  
 請注意，在某些情況下值的範圍並不是連續的。 這是當小數有效位數大於零時增加的小數點所導致。  
  
 只有連接到 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (或更新版本) 伺服器時，DBPARAMFLAGS_SS_ISVARIABLESCALE 才有效。 連接到下層伺服器時，永遠不會設定 DBPARAMFLAGS_SS_ISVARIABLESCALE。  
  
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
  
 當傳送資料到伺服器時，"DBPARAMFLAGS_SS_ISVARIABLESCALE" 會被忽略。 應用程式可以使用提供者特定的類型名稱 "**datetime**" 和 "**smalldatetime**" 來強制使用舊版的表格式資料流 (TDS) 類型。 當連接到 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (或更新版本) 伺服器時，會使用 "**datetime2**" 格式，而且當類型名稱為 "**datetime2**" 或 "DBTYPE_DBTIMESTAMP" 時，會發生隱含的伺服器轉換 (如有必要)。 如果使用了提供者特定的類型名稱 "**datetime**" 或 "**smalldatetime**"，就會忽略 *bScale*。 否則，應用程式必須確保 *bScale* 的設定正確。 從 MDAC 升級的應用程式和從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 升級的 OLE DB Driver for SQL Server 如果會使用 "DBTYPE_DBTIMESTAMP"，但未正確設定 *bScale*，就會失敗。 連接到 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 之前版本的伺服器執行個體時，*bScale* 值如果不是 0 或 3 且具有 "DBTYPE_DBTIMESTAMP"，便是錯誤且會傳回 E_FAIL。  
  
 未呼叫 ICommandWithParameters::SetParameterInfo 時，提供者就會根據 IAccessor::CreateAccessor 中指定的繫結類型來表示伺服器類型，如下所示：  
  
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
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|設定|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|設定|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|設定|  
  
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
  
 只有連接到 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (或更新版本) 伺服器時，DBCOLUMNFLAGS_SS_ISVARIABLESCALE 才有效。 連接到下層伺服器時，不會定義 DBCOLUMNFLAGS_SS_ISVARIABLESCALE。  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 結構會傳回下列資訊：  
  
|參數類型|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|date|DBTYPE_DBDATE|6|10|0|Clear|  
|time(1..7)|DBTYPE_DBTIME2|10|8, 10..16|0..7|設定|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|設定|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|設定|  
  
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
 [對 OLE DB 日期和時間改善的資料類型支援](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
  
  
