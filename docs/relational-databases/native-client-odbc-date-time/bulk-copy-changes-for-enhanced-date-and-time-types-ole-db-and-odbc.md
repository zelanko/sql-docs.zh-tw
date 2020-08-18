---
description: 增強型日期和時間類型的大量複製變更 (OLE DB 和 ODBC)
title: 大量複製、增強型別、OLE DB
ms.custom: ''
ms.date: 12/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, bulk copy operations
ms.assetid: c29e0f5e-9b3c-42b3-9856-755f4510832f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 208cc75e186c0c1de32ed10d263359ffdbb7e039
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423880"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc"></a>增強型日期和時間類型的大量複製變更 (OLE DB 和 ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  本主題描述可支援大量複製功能的日期/時間增強功能。 本主題中的資訊同時適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中的 OLE DB 和 ODBC。  
  
## <a name="format-files"></a>格式檔案  
 以互動方式建立格式檔案時，下表描述用於指定日期/時間類型與對應主檔資料類型名稱的輸入。  
  
|檔案儲存類型|主檔案資料類型|提示的回應：「請輸入欄位 <欄位名稱> [\<default>] 的檔案儲存類型：」|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|Datetime|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|Date|SQLDATE|de|  
|Time|SQLTIME|te|  
|Datetime2|SQLDATETIME2|d2|  
|Datetimeoffset|SQLDATETIMEOFFSET|do|  
||||

 XML 格式檔案 XSD 將具備下列加入項目：  
  
```xml
<xs:complexType name="SQLDATETIME2">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATETIMEOFFSET">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATE">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLTIME">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
```  
  
## <a name="character-data-files"></a>字元資料類型  
 在字元資料檔中，日期和時間值會以資料類型的「資料格式：字串和常值」一節中所述的方式來表示，其中支援 ODBC 的 [Odbc 日期和時間改進](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md) ，或針對 OLE DB [OLE DB 日期和時間改善的資料類型支援](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md) 。  
  
 在原生資料檔中，四個新類型的日期和時間值會表示為其 TDS 標記法，其具有 7 (，因為這是所支援的最大值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而且 bcp 資料檔案不會將這些資料行的小數位數儲存) 。 現有 **datetime** 和 **smalldatetime** 類型的儲存或其表格式資料流 (TDS) 表示法沒有變更。  
  
 對於 OLE DB，不同儲存類型的儲存大小如下所示：  
  
|檔案儲存類型|儲存體大小 (以位元組為單位)|  
|-----------------------|---------------------------|  
|Datetime|8|  
|smalldatetime|4|  
|date|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
|||

 ODBC 的大小如下所示。 請注意，以任何格式或資料檔儲存有效位數是沒有必要的，因為 BCP.exe 永遠會從伺服器擷取有效位數。  
  
|檔案儲存類型|儲存體大小 (以位元組為單位)|儲存體格式|  
|-----------------------|---------------------------|--------------------|  
|datetime (d)|8|表格式資料流 (TDS)|  
|smalldatetime (D)|4|表格式資料流 (TDS)|  
|date (de)|3|表格式資料流 (TDS)|  
|time (te)|6|表格式資料流 (TDS)|  
|datetime2 (d2)|9|表格式資料流 (TDS)|  
|datetimeoffset (do)|11|表格式資料流 (TDS)|  
||||

## <a name="bcp-types-in-sqlnclih"></a>sqlncli.h 中的 BCP 類型  
 下列類型是在 sqlncli.h 中定義的，可與 ODBC 的 BCP API 延伸模組搭配使用。 這些類型會利用 OLE DB 中 IBCPSession::BCPColFmt 的 *eUserDataType* 參數來傳遞。  
  
|檔案儲存類型|主檔案資料類型|輸入 sqlncli，以搭配 IBCPSession：： BCPColFmt 使用|值|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|Datetime|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIME4|0x3a|  
|Date|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Time|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
|||||

## <a name="bcp-data-type-conversions"></a>BCP 資料類型轉換  
 下表提供轉換資訊。  
  
 **OLE DB 注意**：下列轉換是由 IBCPSession 所執行。 IRowsetFastLoad 會使用如[從用戶端到伺服器執行的轉換](../../relational-databases/native-client-ole-db-date-time/conversions-performed-from-client-to-server.md)中所定義的 OLE DB 轉換。 請注意，datetime 值會捨入為一秒的 1/300，而 smalldatetime 值在執行以下所描述的用戶端轉換之後，會將其秒數設定為零。 Datetime 捨入會透過小時和分鐘 (但非日期) 傳播。  
  
|目標 --><br /><br /> 從|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|Date|1|-|1,6|1,6|1,6|1,5,6|1,3|1,3|  
|Time|N/A|1,10|1,7,10|1,7,10|1,7,10|1,5,7,10|1,3|1,3|  
|Smalldatetime|1,2|1,4,10|1|1|1,10|1,5,10|1,11|1,11|  
|Datetime|1,2|1,4,10|1,12|1|1,10|1,5,10|1,11|1,11|  
|Datetime2|1,2|1,4,10|1,10 (ODBC)1,12 (OLE DB)|1,10|1,10|1,5,10|1,3|1,3|  
|Datetimeoffset|1,2,8|1,4,8,10|1,8,10|1,8,10|1,8,10|1,10|1,3|1,3|  
|Char/wchar (date)|9|-|9,6 (ODBC)9,6,12 (OLE DB)|9,6 (ODBC)9,6,12 (OLE DB)|9,6|9,5,6|N/A|N/A|  
|Char/wchar (time)|-|9,10|9,7,10 (ODBC)9,7,10,12 (OLE DB)|9,7,10 (ODBC)9,7,10, 12 (OLE DB)|9,7,10|9,5,7,10|N/A|N/A|  
|Char/wchar (datetime)|9,2|9,4,10|9,10 (ODBC)9,10,12 (OLE DB)|9,10 (ODBC)9,10,12 (OLE DB)|9,10|9,5,10|N/A|N/A|  
|Char/wchar (datetimeoffset)|9,2,8|9,4,8,10|9,8,10 (ODBC)9,8,10,12 (OLE DB)|9,8,10 (ODBC)9,8,10,12 (OLE DB)|9,8,10|9,10|N/A|N/A|  
||||||||||

#### <a name="key-to-symbols"></a>符號的索引鍵  
  
|符號|意義|  
|------------|-------------|  
|-|不支援轉換。<br /><br /> 系統會產生含有 SQLSTATE 07006 和訊息「限制的資料類型屬性違規」的 ODBC 診斷記錄。|  
|1|如果提供的資料無效，就會產生含有 SQLSTATE 22007 和訊息「無效的 datetime 格式」的 ODBC 診斷記錄。 對於 datetimeoffset 值，即使沒有要求轉換為 UTC，此時間部分在轉換到 UTC 之後仍然必須在範圍內。 這是因為 TDS 和伺服器永遠會以 UTC 的 datetimeoffset 值，正規化時間。 因此，用戶端必須確認時間元件在轉換為 UTC 之後，仍然位於支援的範圍內。|  
|2|忽略時間元件。|  
|3|針對 ODBC，如果發生資料遺失的截斷，就會產生含有 SQLSTATE 22001 和訊息「字串資料，右邊已截斷」的診斷記錄，小數位數 (小數位數) 根據下表，從目的地資料行的大小決定。 對於大於資料表中範圍的資料行大小，就會隱含小數位數 7。 此轉換應該最多允許九個小數秒位數，也就是 ODBC 所允許的最大值。<br /><br /> **類型：** DBTIME2<br /><br /> **隱含的小數位數 0：** 8<br /><br /> **隱含的小數位數 1. 7** 10、16<br /><br /> <br /><br /> **類型：** DBTIMESTAMP<br /><br /> **隱含的範圍 0：** 19<br /><br /> **隱含的小數位數 1. 7：** 21. 27<br /><br /> <br /><br /> **類型：** DBTIMESTAMPOFFSET<br /><br /> **隱含的範圍 0：** 26<br /><br /> **隱含的小數位數 1. 7：** 28. 34<br /><br /> 對於 OLE DB，如果截斷時發生資料損失，則會發佈錯誤。 對於 datetime2，小數秒的位數 (小數位數) 會根據下表，從目的地資料行的大小決定。 對於大於資料表中範圍的資料行大小，就會隱含小數位數 9。 此轉換應該最多允許九個小數秒位數，也就是 OLE DB 所允許的最大值。<br /><br /> **類型：** DBTIME2<br /><br /> **隱含的小數位數 0：** 8<br /><br /> **隱含的小數位數 1..9：** 1..9<br /><br /> <br /><br /> **類型：** DBTIMESTAMP<br /><br /> **隱含的範圍 0：** 19<br /><br /> **隱含的範圍 1..9：** 21..29<br /><br /> <br /><br /> **類型：** DBTIMESTAMPOFFSET<br /><br /> **隱含的範圍 0：** 26<br /><br /> **隱含的範圍 1..9：** 28..36|  
|4|忽略日期元件。|  
|5|時區會設定為 UTC (例如，00:00)。|  
|6|時間會設定為零。|  
|7|日期會設定為 1900-01-01。|  
|8|忽略時區位移。|  
|9|根據出現的第一個標點符號字元以及剩餘的元件是否存在，字串會經過剖析，並轉換為 date、datetime、datetimeoffset 或 time 值。 接著，在此程序針對來源類型探索本主題結尾之資料表中的規則之後，此字串會轉換為目標類型。 如果剖析提供的資料時一定會發生錯誤，或如果任何元件部分超出允許的範圍之外，或如果沒有從常值類型轉換為目標類型，就會發佈錯誤 (OLE DB)，會產生包含 SQLSTATE 22018 和訊息「轉換規格的字元值無效」的 ODBC 診斷記錄。 對於 datetime 和 smalldatetime 參數，如果年份超出這些類型支援的範圍，就會發佈錯誤 (OLE DB)，或產生含有 SQLSATE 22007 和訊息「無效的 datetime 格式」的 ODBC 診斷記錄。<br /><br /> 對於 datetimeoffset，即使沒有要求轉換為 UTC，此值在轉換到 UTC 之後仍然必須在範圍內。 這是因為 TDS 和伺服器永遠會以 UTC 的 datetimeoffset 值，將時間正規化，因此用戶端必須在轉換成 UTC 之後，確認時間元件位於支援的範圍內。 如果此值不在支援的 UTC 範圍內，就會發佈錯誤 (OLE DB)，或產生含有 SQLSTATE 22007 和訊息「無效的 datetime 格式」的 ODBC 診斷記錄。|  
|10|如果在從用戶端轉換為伺服器時發生資料遺失的截斷，就會發佈錯誤 (OLE DB)，或產生包含 SQLSTATE 22008 以及「日期時間欄位溢位」訊息的 ODBC 診斷記錄。 如果此值落在伺服器使用之 UTC 範圍所代表的範圍外，也可能發生這個錯誤。 如果在從伺服器轉換為用戶端時發生秒或小數秒的截斷，只會有一個警告。|  
|11|如果截斷時發生資料損失，則會產生診斷記錄。<br /><br /> 在伺服器轉換為用戶端時，這是一個警告 (ODBC SQLSTATE S1000)。<br /><br /> 在用戶端轉換為伺服器時，這是一個錯誤 (ODBC SQLSTATE 22001)。|  
|12|秒數會設定為零，而小數秒會遭到捨棄。 不可能發生截斷錯誤。|  
|N/A|系統會維持現有 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和舊有的行為。|  
|||

## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;的日期和時間改進 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)   
 [日期和時間改善 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
