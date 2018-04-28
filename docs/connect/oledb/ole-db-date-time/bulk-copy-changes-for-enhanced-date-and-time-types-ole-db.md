---
title: 大量複製變更對增強的日期和時間類型 (OLE DB) |Microsoft 文件
description: 增強型的日期和時間類型 (OLE DB) 的大量複製變更
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
- OLE DB, bulk copy operations
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bebddc7a9ad8dc7d59f60fab73bcdca8b1192dab
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db"></a>增強型的日期和時間類型 (OLE DB) 的大量複製變更
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本文描述 SQL Server 的 OLE DB 驅動程式中支援大量複製功能的日期/時間增強功能。  
  
## <a name="format-files"></a>格式檔案  
 以互動方式建立格式檔案時，下表描述用於指定日期/時間類型與對應主檔資料類型名稱的輸入。  
  
|檔案儲存類型|主檔案資料類型|提示的回應: 「 輸入欄位 < field_name > 檔案儲存類型 [\<預設 >]:"|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|Datetime|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|日期|SQLDATE|de|  
|Time|SQLTIME|te|  
|Datetime2|SQLDATETIME2|d2|  
|Datetimeoffset|SQLDATETIMEOFFSET|do|  
  
 XML 格式檔案 XSD 將具備下列加入項目：  
  
```  
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
 在字元資料檔中，日期和時間值的表示如 「 資料格式： 字串和常值 」 一節中所述[OLE DB 日期和時間增強功能的資料類型支援](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)for OLE DB。  
  
 在原生資料檔案中，四個新類型的日期和時間值會表示為 TDS 表示法小數位數 7 (因為這是支援的最大值[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]和 bcp 資料檔不會儲存這些資料行的小數位數)。 沒有任何變更的現有儲存體**datetime**和**smalldatetime**類型或其表格式資料流 (TDS) 表示法。  
  
 對於 OLE DB，不同儲存類型的儲存大小如下所示：  
  
|檔案儲存類型|儲存體大小 (以位元組為單位)|  
|-----------------------|---------------------------|  
|datetime|8|  
|smalldatetime|4|  
|date|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
 
  
## <a name="bcp-types-in-msoledbsqlh"></a>Msoledbsql.h 中的 BCP 類型  
 下列類型 msoledbsql.h 中定義。 這些類型會隨*eUserDataType* ibcpsession:: Bcpcolfmt OLE DB 中的參數。  
  
|檔案儲存類型|主檔案資料類型|輸入用於 ibcpsession:: Bcpcolfmt msoledbsql.h|Value|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|Datetime|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIM4|0x3a|  
|日期|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Time|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>BCP 資料類型轉換  
 下表提供轉換資訊。  
  
 **OLE DB 注意**IBCPSession 所執行的下列轉換。 IRowsetFastLoad 中所定義，請使用 OLE DB 轉換[轉換從用戶端到伺服器執行](../../oledb/ole-db-date-time/conversions-performed-from-client-to-server.md)。 請注意，datetime 值會捨入為一秒的 1/300，而 smalldatetime 值在執行以下所描述的用戶端轉換之後，會將其秒數設定為零。 Datetime 捨入會透過小時和分鐘 (但非日期) 傳播。  
  
|目標 --><br /><br /> 來源|date|time|smalldatetime|datetime|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|日期|1|-|1, 6|1, 6|1, 6|1、 5、 6|1, 3|1, 3|  
|Time|해당 사항 없음|1, 10|1，7 10|1，7 10|1，7 10|1、 5、 7、 10|1, 3|1, 3|  
|Smalldatetime|1, 2|1、 4、 10|1|1|1, 10|1、 5、 10|1, 11|1, 11|  
|Datetime|1, 2|1、 4、 10|1, 12|1|1, 10|1、 5、 10|1, 11|1, 11|  
|Datetime2|1, 2|1、 4、 10|1, 12|1, 10|1, 10|1、 5、 10|1, 3|1, 3|  
|Datetimeoffset|1, 2, 8|1、 4、 8、 10|1、 8、 10|1、 8、 10|1、 8、 10|1, 10|1, 3|1, 3|  
|Char/wchar (date)|9|-|9、 6、 12|9、 6、 12|9、 6|9、 5、 6|해당 사항 없음|해당 사항 없음|  
|Char/wchar (time)|-|9, 10|9、 7、 10、 12|9、 7、 10、 12|9、 7、 10|9、 5、 7、 10|해당 사항 없음|해당 사항 없음|  
|Char/wchar (datetime)|9, 2|9、 4、 10|9、 10、 12|9、 10、 12|9, 10|9、 5、 10|해당 사항 없음|해당 사항 없음|  
|Char/wchar (datetimeoffset)|9, 2, 8|9、 4、 8、 10|9、 8、 10、 12|9、 8、 10、 12|9、 8、 10|9, 10|해당 사항 없음|N/A|  
  
#### <a name="key-to-symbols"></a>符號的索引鍵  
  
|符號|意義|  
|------------|-------------|  
|-|不支援轉換。<br />|  
|1|如果提供的資料不是有效的就會發佈錯誤。 對於 datetimeoffset 值，即使沒有要求轉換為 UTC，此時間部分在轉換到 UTC 之後仍然必須在範圍內。 這是因為 TDS 和伺服器永遠會以 UTC 的 datetimeoffset 值，正規化時間。 因此，用戶端必須確認時間元件在轉換為 UTC 之後，仍然位於支援的範圍內。|  
|2|忽略時間元件。|  
|3|如果發生資料遺失的截斷，就會發佈錯誤。 對於 datetime2，小數秒的位數 (小數位數) 會根據下表，從目的地資料行的大小決定。 對於大於資料表中範圍的資料行大小，會隱含小數位數 9。 此轉換應該最多允許九個小數秒位數，也就是 OLE DB 所允許的最大值。<br /><br /> **類型：** DBTIME2<br /><br /> **隱含的小數位數 0** 8<br /><br /> **隱含的小數位數 1..9** 1..9<br /><br /> <br /><br /> **類型：** DBTIMESTAMP<br /><br /> **隱含的小數位數 0:** 19<br /><br /> **隱含的小數位數 1..9:** 21..29<br /><br /> <br /><br /> **類型：** DBTIMESTAMPOFFSET<br /><br /> **隱含的小數位數 0:** 26<br /><br /> **隱含的小數位數 1..9:** 28..36|  
|4|忽略日期元件。|  
|5|時區會設定為 UTC (例如，00:00)。|  
|6|時間會設定為零。|  
|7|日期會設定為 1900-01-01。|  
|8|忽略時區位移。|  
|9|根據出現的第一個標點符號字元以及剩餘的元件是否存在，字串會經過剖析，並轉換為 date、datetime、datetimeoffset 或 time 值。 接著，將此字串轉換成目標類型，依照此程序探索來源類型的這篇文章結尾處資料表中的規則。 如果無法剖析提供的資料，而沒有錯誤，或如果任何元件部分超出允許的範圍，或如果沒有從常值類型轉換成目標型別，就會發佈錯誤。 對於 datetime 和 smalldatetime 參數，如果年份超出這些類型支援，範圍會發佈錯誤。<br /><br /> 對於 datetimeoffset，即使沒有要求轉換為 UTC，此值在轉換到 UTC 之後仍然必須在範圍內。 這是因為 TDS 和伺服器永遠會以 UTC 的 datetimeoffset 值，將時間正規化，因此用戶端必須在轉換成 UTC 之後，確認時間元件位於支援的範圍內。 如果值不是支援的 UTC 範圍內，就會發佈錯誤。|  
|10|用戶端與伺服器之間的轉換中，如果截斷時發生資料遺失就會發佈錯誤。 如果此值落在伺服器使用之 UTC 範圍所代表的範圍外，也可能發生這個錯誤。 如果在從伺服器轉換為用戶端時發生秒或小數秒的截斷，只會有一個警告。|  
|11|用戶端與伺服器之間的轉換中，如果截斷時發生資料遺失就會發佈錯誤。|
|12|秒數會設定為零，而小數秒會遭到捨棄。 不可能發生截斷錯誤。|  
|해당 사항 없음|系統會維持現有 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和舊有的行為。|  
  
## <a name="see-also"></a>另請參閱     
 [日期和時間增強功能 & #40; OLE DB & #41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
