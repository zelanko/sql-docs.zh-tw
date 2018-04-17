---
title: 執行轉換，因此從用戶端到伺服器 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB], client to server
ms.assetid: 6bb24928-0f3e-4119-beda-cfd04a44a3eb
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f33ac306e40582639f09572d570cbd6a5032594d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="conversions-performed-from-client-to-server"></a>從用戶端到伺服器執行的轉換
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主題描述在以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 撰寫之用戶端應用程式和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (或更新版本) 之間執行的日期/時間轉換。  
  
## <a name="conversions"></a>轉換  
 本主題描述針對用戶端所進行的轉換。 如果用戶端針對參數所指定的小數秒有效位數與伺服器上所定義的小數秒有效位數不同，在伺服器允許作業成功的情況下，用戶端轉換可能會造成失敗。 特別是，用戶端會將任何截斷的小數秒視為錯誤，而[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時間捨去為最接近的整秒的值。  
  
 如果未呼叫 icommandwithparameters:: Setparameterinfo，DBTYPE_DBTIMESTAMP 繫結會轉換就如同**datetime2**。  
  
|目標 -><br /><br /> 來源|DBDATE (date)|DBTIME (time)|DBTIME2 (time)|DBTIMESTAMP (smalldatetime)|DBTIMESTAMP (datetime)|DBTIMESTAMP (datetime2)|DBTIMESTAMPOFFSET (datetimeoffset)|STR|WSTR|SQLVARIANT<br /><br /> (sql_variant)|  
|----------------------|---------------------|---------------------|----------------------|-----------------------------------|------------------------------|-------------------------------|------------------------------------------|---------|----------|-------------------------------------|  
|DATE|1,2|1,3,4|4,12|1,12|1,12|1,12|1,5, 12|1,12|1,12|1,12<br /><br /> datetime2(0)|  
|DBDATE|1|-|-|1,6|1,6|1,6|1,5, 6|1,10|1,10|1<br /><br /> date|  
|DBTIME|-|1|1|1,7|1,7|1,7|1,5, 7|1,10|1,10|1<br /><br /> Time(0)|  
|DBTIME2|-|1,3|1|1,7,10,14|1,7,10,15|1,7,10|1,5,7,10|1,10,11|1,10,11|1<br /><br /> Time(7)|  
|DBTIMESTAMP|1,2|1,3,4|1,4,10|1,10,14|1,10,15|1,10|1,5,10|1,10,11|1,10,11|1,10<br /><br /> datetime2(7)|  
|DBTIMESTAMPOFFSET|1,2,8|1,3,4,8|1,4,8,10|1,8,10,14|1,8,10,15|1,8,10|1,10|1,10,11|1,10,11|1,10<br /><br /> datetimeoffset(7)|  
|FILETIME|1,2|1,3,4|1,4,13|1,13|1,13|1,13|1,5,13|1,13|1,10|1,13<br /><br /> datetime2(3)|  
|BYTES|-|-|-|-|-|-|-|해당 사항 없음|不適用|해당 사항 없음|  
|VARIANT|1|1|1|1,10|1,10|1,10|1,10|해당 사항 없음|해당 사항 없음|1,10|  
|SSVARIANT|1,16|1,16|1,16|1,10,16|1,10,16|1,10,16|1,10,16|해당 사항 없음|N/A|1,16|  
|BSTR|1,9|1,9|1,9,10|1,9,10|1,9,10|1,9,10|1,9,10|해당 사항 없음|不適用|해당 사항 없음|  
|STR|1,9|1,9|1,9,10|1,9,10|1,9,10|1,9,10|1,9,10|해당 사항 없음|不適用|해당 사항 없음|  
|WSTR|1,9|1,9|1,9,10|1,9,10|1,9,10|1,9,10|1,9,10|해당 사항 없음|不適用|N/A|  
  
## <a name="key-to-symbols"></a>符號的索引鍵  
  
|符號|意義|  
|------------|-------------|  
|-|不支援轉換。 如果繫結驗證時 iaccessor:: Createaccessor 呼叫時，就會傳回 DBBINDSTATUS_UPSUPPORTEDCONVERSION *rgStatus*。 當存取子驗證延遲時，會設定 DBSTATUS_E_BADACCESSOR。|  
|해당 사항 없음|不適用。|  
|1|如果提供的資料無效，則會設定 DBSTATUS_E_CANTCONVERTVALUE。 輸入資料會在套用轉換之前進行驗證，因此，即使在後續轉換忽略元件時，該資料仍然必須有效，轉換才會成功。|  
|2|忽略時間欄位。|  
|3|小數秒必須為，否則會設定 DBSTATUS_E_DATAOVERFLOW。|  
|4|忽略日期元件。|  
|5|時區會設定為用戶端的時區設定。|  
|6|時間會設定為零。|  
|7|日期會設定為目前的日期。|  
|8|時間會轉換成 UTC。 如果此轉換期間發生錯誤，則會設定 DBSTATUS_E_CANTCONVERTVALUE。|  
|9|此字串會剖析為 ISO 常值，並轉換為目標類型。 如果失敗，字串會剖析為 OLE 日期常值 (也有時間元件)，並從 OLE 日期 (DBTYPE_DATE) 轉換為目標類型。<br /><br /> 如果目標類型為 DBTIMESTAMP、 **smalldatetime**、 **datetime**或 **datetime2**，字串必須符合日期、時間或 **datetime2** 常值的語法，或者是 OLE 所識別的語法。 如果字串為日期常值，所有時間元件都會設定為零。 如果字串為時間常值，日期會設定目前的日期。<br /><br /> 對於其他所有目標類型，字串必須符合目標類型之常值的語法。|  
|10|如果截斷的小數秒發生資料遺失，則會設定 DBSTATUS_E_DATAOVERFLOW。 對於字串轉換，只有在字串符合 ISO 語法時，才能進行溢位檢查。 如果字串為 OLE 日期常值，會捨去小數秒。<br /><br /> 為從 DBTIMESTAMP (datetime) 到 smalldatetime 的轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端將會以無訊息模式截斷秒數值，而非引發 DBSTATUS_E_DATAOVERFLOW 錯誤。|  
|11|小數秒位數 （小數位數） 的數目是根據下表決定從目的地資料行的大小。 對於大於資料表中範圍的資料行大小，會隱含小數位數 9。 此轉換應該最多允許九個小數秒位數，也就是 OLE DB 所允許的最大值。<br /><br /> 不過，如果來源類型為 DBTIMESTAMP 而且小數秒為零，則不會產生任何小數秒位數或小數點。 此行為可確保使用舊版 OLE DB 提供者所開發之應用程式的回溯相容性。<br /><br /> 資料行大小 ~0 在 OLE DB 中隱含為大小無限制 (除非 DBTIMESTAMP 套用 3 位數規則，否則為 9 位數)。|  
|12|之前的轉換語意[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]針對 DBTYPE_DATE 維護。 小數秒會截斷到零。|  
|13|之前的轉換語意[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]會針對 DBTYPE_FILETIME 維護。 如果您使用 Windows FileTimeToSystemTime API，小數秒有效位數是限制為 1 毫秒。|  
|14|之前的轉換語意[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]如**smalldatetime**進行維護。 秒數會設定為零。|  
|15|之前的轉換語意[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]如**datetime**進行維護。 描述會捨去為第 300 個最接近的秒數。|  
|16|內嵌在 SSVARIANT 用戶端架構中之值 (屬於給定類型) 的轉換行為與未內嵌在 SSVARIANT 用戶端架構時之值和類型的行為相同。|  
  
||||  
|-|-|-|  
|型別|長度 (以字元為單位)|小數位數|  
|DBTIME2|8, 10..18|0,1..9|  
|DBTIMESTAMP|19, 21..29|0,1..9|  
|DBTIMESTAMPOFFSET|26, 28..36|0,1..9|  
  
## <a name="see-also"></a>另請參閱  
 [繫結和轉換&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
  
  
