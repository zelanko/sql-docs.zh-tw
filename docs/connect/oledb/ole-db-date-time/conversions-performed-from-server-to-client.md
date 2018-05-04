---
title: 執行轉換，從伺服器到用戶端 |Microsoft 文件
description: 從伺服器到用戶端執行的轉換
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [OLE DB], server to client
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: cada710747fb2ec9431ef54ae0108db36e596773
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="conversions-performed-from-server-to-client"></a>從伺服器到用戶端執行的轉換
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  這篇文章描述之間執行的日期/時間轉換[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]（或更新版本） 和 SQL Server 的撰寫與 OLE DB 驅動程式的用戶端應用程式。  
  
## <a name="conversions"></a>轉換  
 下表描述傳回用戶端之類行與繫結中之類型之間的轉換。 對於輸出參數，如果已呼叫 icommandwithparameters:: Setparameterinfo，而且在指定的型別*pwszDataSourceType*不的符合伺服器將會執行實際的型別，在伺服器上，隱含的轉換並傳回至用戶端的類型會比對 icommandwithparameters:: Setparameterinfo 透過指定的型別。 這可能會導致非預期的轉換結果時這篇文章中描述的不同伺服器的轉換規則。 例如，必須提供預設日期時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會使用 1900-1-1 而非 1899-12-30。  
  
|目標 -><br /><br /> 來源|DATE|DBDATE|DBTIME|DBTIME2|DBTIMESTAMP|DBTIMESTAMPOFFSET|FILETIME|BYTES|VARIANT|SSVARIANT|BSTR|STR|WSTR|  
|----------------------|----------|------------|------------|-------------|-----------------|-----------------------|--------------|-----------|-------------|---------------|----------|---------|----------|  
|日期|1, 7|確定|-|-|1|1, 3|1, 7|-|[確定] (VT_BSTR)|確定|確定|4|4|  
|Time|5、 6、 7|-|9|確定|6|3, 6|5、 6|-|[確定] (VT_BSTR)|確定|確定|4|4|  
|Smalldatetime|7|8|9, 10|10|確定|3|7|-|7 (VT_DATE)|確定|確定|4|4|  
|Datetime|5、 7|8|9, 10|10|確定|3|7|-|7 (VT_DATE)|確定|確定|4|4|  
|Datetime2|5、 7|8|9, 10|10|7|3|5、 7|-|[確定] (VT_BSTR)|確定|確定|4|4|  
|Datetimeoffset|5、 7、 11|8, 11|9、 10、 11|10、 11|7, 11|確定|5、 7、 11|-|[確定] (VT_BSTR)|確定|確定|4|4|  
|Char, Varchar,<br /><br /> Nchar, Nvarchar|7, 13|12|12 9|12|12|12|7, 13|해당 사항 없음|不適用|不適用|不適用|不適用|해당 사항 없음|  
|Sql_variant<br /><br /> (datetime)|7|8|9, 10|10|確定|3|7|-|7 (VT_DATE)|確定|確定|4|4|  
|Sql_variant<br /><br /> (smalldatetime)|7|8|9, 10|10|確定|3|7|-|7 (VT_DATE)|確定|確定|4|4|  
|Sql_variant<br /><br /> (date)|1, 7|確定|2|2|1|1, 3|1, 7|-|OK(VT_BSTR)|確定|確定|4|4|  
|Sql_variant<br /><br /> (time)|5、 6、 7|2|6|確定|6|3, 6|5、 6|-|OK(VT_BSTR)|確定|確定|4|4|  
|Sql_variant<br /><br /> (datetime2)|5、 7|8|9, 10|10|確定|3|5、 7|-|OK(VT_BSTR)|確定|確定|4|4|  
|Sql_variant<br /><br /> (datetimeoffset)|5、 7、 11|8, 11|9、 10、 11|10、 11|7, 11|確定|5、 7、 11|-|OK(VT_BSTR)|確定|確定|4|4|  
  
## <a name="key-to-symbols"></a>符號的索引鍵  
  
|符號|意義|  
|------------|-------------|  
|確定|不需要任何轉換。|  
|-|不支援轉換。 如果繫結驗證時 iaccessor:: Createaccessor 呼叫時，就會傳回 DBBINDSTATUS_UPSUPPORTEDCONVERSION *rgStatus*。 當存取子驗證延遲時，會設定 DBSTATUS_E_BADACCESSOR。|  
|1|時間欄位會設定為零。|  
|2|DBSTATUS_E_CANTCONVERTVALUE 已設定。|  
|3|時區會設定為零。|  
|4|如果用戶端緩衝區不夠大，會設定 DBSTATUS_S_TRUNCATED。 當伺服器類型包含小數秒時，結果字串中的位數會完全符合伺服器類型的小數位數。|  
|5|截斷的秒數或小數秒數會被忽略。|  
|6|除非來源為字串時間常值，而且目的地為 DBTYPE_DATE，否則日期會設定為目前的日期。 在此情況下，會使用 1899-12-30。|  
|7|如果值溢位，會設定 DBSTATUS_E_DATAOVERFLOW。|  
|8|忽略時間欄位。|  
|9|忽略小數秒欄位。|  
|10|忽略日期元件。|  
|11|時間會轉換成用戶端時區。 如果此轉換期間發生錯誤，則會設定 DBSTATUS_E_DATAOVERFLOW。|  
|12|此字串會剖析為 ISO 常值，並轉換為目標類型。 如果失敗，字串會剖析為 OLE 日期常值 (也有時間元件)，並從 OLE 日期 (DBTYPE_DATE) 轉換為目標類型。 字串必須符合進行 ISO 格式剖析所允許之目標類型常值的語法才會成功。 若要讓 OLE 剖析成功，字串必須符合 OLE 所識別的語法。 如果無法剖析字串，則會設定 DBSTATUS_E_CANTCONVERTVALUE。 如果任何元件值超出範圍，會設定 DBSTATUS_E_DATAOVERFLOW。|  
|13|此字串會剖析為 ISO 常值，並轉換為目標類型。 如果失敗，字串會剖析為 OLE 日期常值 (也有時間元件)，並從 OLE 日期 (DBTYPE_DATE) 轉換為目標類型。 除非目的地為 DBTYPE_DATE 或 DBTYPE_DBTIMESTAMP，否則字串必須符合日期時間常值的語法。 如果是這種狀況，ISO 格式剖析允許使用日期時間或時間嘗試才會成功。 若要讓 OLE 剖析成功，字串必須符合 OLE 所識別的語法。 如果無法剖析字串，則會設定 DBSTATUS_E_CANTCONVERTVALUE。 如果任何元件值超出範圍，會設定 DBSTATUS_E_DATAOVERFLOW。|  
  
## <a name="see-also"></a>另請參閱  
 [繫結和轉換&#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
  
  
