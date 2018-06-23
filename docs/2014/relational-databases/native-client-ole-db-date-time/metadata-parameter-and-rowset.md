---
title: 參數和資料列集的中繼資料 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
ms.assetid: 31b318a4-20e7-4db0-b367-eb9938859029
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a8b3365cdf3a2773b6627dfd49edd20b839ef9a8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36147150"
---
# <a name="parameter-and-rowset-metadata"></a>參數和資料列集中繼資料
  本主題提供有關下列與 OLE DB 日期和時間增強功能相關之類型和類型成員的資訊。  
  
-   DBBINDING 結構  
  
-   `ICommandWithParameters::GetParameterInfo`  
  
-   `ICommandWithParameters::SetParameterInfo`  
  
-   `IColumnsRowset::GetColumnsRowset`  
  
-   `IColumnsInfo::GetColumnInfo`  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 下列資訊會以 DBPARAMINFO 結構透過傳回*prgParamInfo*:  
  
|參數類型|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|-------------------|------------------|--------------|-----------------------------------------------------|  
|日期|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|將|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19,21..27|0..7|將|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26,28..34|0..7|將|  
  
 請注意，在某些情況下值的範圍並不是連續的。 這是當小數有效位數大於零時增加的小數點所導致。  
  
 DBPARAMFLAGS_SS_ISVARIABLESCALE 才有效，當連接到[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更新版本） 伺服器。 連接到下層伺服器時，絕對不會設定 DBPARAMFLAGS_SS_ISVARIABLESCALE。  
  
## <a name="icommandwithparameterssetparameterinfo-and-implied-parameter-types"></a>ICommandWithParameters::SetParameterInfo 和隱含參數類型  
 以 DBPARAMBINDINFO 結構所提供的資訊必須與下列相符：  
  
|*pwszDataSourceType*<br /><br /> (提供者特定)|*pwszDataSourceType*<br /><br /> (OLE DB 一般)|*ulParamSize*|*bScale*|  
|----------------------------------------------------|-------------------------------------------------|-------------------|--------------|  
||DBTYPE_DATE|6|忽略|  
|日期|DBTYPE_DBDATE|6|忽略|  
||DBTYPE_DBTIME|10|忽略|  
|time|DBTYPE_DBTIME2|10|0..7|  
|smalldatetime||16|忽略|  
|DATETIME||16|忽略|  
|datetime2 或 DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|16|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|0..7|  
  
 *BPrecision*參數已忽略。  
  
 當傳送資料到伺服器時，"DBPARAMFLAGS_SS_ISVARIABLESCALE" 會被忽略。 應用程式可以使用提供者特定的類型名稱 "`datetime`" 和 "`smalldatetime`" 來強制使用舊版的表格式資料流 (TDS) 類型。 當連接到[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更新版本） 伺服器，「`datetime2`"將會使用格式和隱含伺服器會進行轉換，如有必要，當類型名稱為"`datetime2`"或"DBTYPE_DBTIMESTAMP"。 *bScale*如果提供者特定的類型名稱則會忽略"`datetime`「 或 」`smalldatetime`」 可用。 否則，應用程式必須確保*bScale*已正確設定。 從 MDAC 升級的應用程式和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端從[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]"DBTYPE_DBTIMESTAMP"將會失敗，如果它們不會設定的使用*bScale*正確。 當連接到伺服器執行個體早於[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 *bScale* 0 或 3 且具有"DBTYPE_DBTIMESTAMP"以外的值是錯誤，而且不會傳回 E_FAIL。  
  
 不呼叫 icommandwithparameters:: Setparameterinfo 時，提供者推斷伺服器類型從 iaccessor:: Createaccessor 中所指定的繫結類型，如下所示：  
  
|繫結類型|*pwszDataSourceType*<br /><br /> (提供者特定)|  
|------------------|----------------------------------------------------|  
|DBTYPE_DATE|datetime2(0)|  
|DBTYPE_DBDATE|日期|  
|DBTYPE_DBTIME|time(0)|  
|DBTYPE_DBTIME2|time(7)|  
|DBTYPE_DBTIMESTAMP|datetime2(7)|  
|DBTYPE_DBTIMESTAMPOFFSET|datetimeoffset(7)|  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 `IColumnsRowset::GetColumnsRowset` 傳回下列資料行：  
  
|資料行類型|DBCOLUMN_TYPE|DBCOLUM_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE、DBCOLUMN_DATETIMEPRECISION|DBCOLUMN_FLAGS, DBCOLUMNFLAGS_SS_ISVARIABLESCALE|  
|-----------------|--------------------|-------------------------|-------------------------|--------------------------------------------------|---------------------------------------------------------|  
|日期|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|將|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|將|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|將|  
  
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
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE 才有效，當連接到[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更新版本） 伺服器。 連接到下層伺服器時，不會定義 DBCOLUMNFLAGS_SS_ISVARIABLESCALE。  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 結構會傳回下列資訊：  
  
|參數類型|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|日期|DBTYPE_DBDATE|6|10|0|Clear|  
|time(1..7)|DBTYPE_DBTIME2|10|8, 10..16|0..7|將|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|將|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|將|  
  
 在*dwFlags*、 DBCOLUMNFLAGS_ISFIXEDLENGTH 一定是 true。 日期/時間類型，而且下列旗標永遠為 false:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER, MAYDEFER  
  
 可以設定剩餘的旗標 (DBCOLUMNFLAGS_ISNULLABLE、DBCOLUMNFLAGS_MAYBENULL、DBCOLUMNFLAGS_WRITE 和 DBCOLUMNFLAGS_WRITEUNKNOWN)。  
  
 新的旗標 DBCOLUMNFLAGS_SS_ISVARIABLESCALE 所提供的*dwFlags*以允許應用程式判斷伺服器類型的資料行，其中*wType*是 DBTYPE_DBTIMESTAMP。 *bScale*也必須用來識別伺服器類型。  
  
## <a name="see-also"></a>另請參閱  
 [中繼資料&#40;OLE DB&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
  
  