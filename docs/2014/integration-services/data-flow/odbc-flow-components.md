---
title: ODBC 流程元件 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cf751f1e-2348-4a77-904c-bd92c0d7d0ae
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5466587560477d331e475cf8d32488757975b730
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52764300"
---
# <a name="odbc-flow-components"></a>ODBC 流程元件
  此主題描述使用 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]  
  
 適用於 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 的 Connector for Open Database Connectivity (ODBC) by Attunity 有助於 SSIS 開發人員輕鬆建立封裝，從 ODBC 支援的資料庫載入及卸載資料。  
  
 此 ODBC 連接器設計目的是為了在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]內容中對 ODBC 支援的資料庫載入或卸載資料時達到最佳效能。  
  
## <a name="benefits"></a>優點  
 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 的 ODBC 來源和 ODBC 目的地為 SSIS 專案處理對 ODBC 支援的資料庫載入或卸載資料，提供競爭優勢。  
  
 ODBC 來源和 ODBC 目的地啟用高效能資料與啟用 ODBC 資料庫的整合。 這兩個元件都可以設定為將資料列取向的參數陣列繫結用於支援此繫結模式的高功能 ODBC 提供者，而將單一資料列的參數繫結用於低功能 ODBC 提供者。  
  
## <a name="getting-started-with-the-odbc-source-and-destination"></a>開始使用 ODBC 來源和目的地  
 在設定使用 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]的封裝之前，您必須確認具備下列項目。  
  
-   [ODBC 來源](odbc-source.md)  
  
-   [ODBC 目的地](odbc-destination.md)  
  
 ODBC 來源和 ODBC 目的地提供一種簡單的方式，可從 ODBC 支援的來源資料庫載入及轉換資料至 ODBC 支援的目的地資料庫。  
  
 若要使用來源或目的地載入或卸載資料，請在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中開啟新的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]專案。 然後將來源或目的地拖曳至 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的設計介面。  
  
-   ODBC 來源元件會從 ODBC 支援的來源資料庫讀取資料。  
  
 您可以將 ODBC 來源連接到 SSIS 支援的任何目的地或轉換元件。  
  
 **另請參閱：**  
  
 ODBC 來源  
  
 ODBC 來源編輯器 (連線管理員頁面)  
  
 ODBC 來源編輯器 (錯誤輸出頁面)  
  
-   ODBC 目的地會將資料載入 ODBC 支援的資料庫。 您可以將此目的地連接到 SSIS 支援的任何來源或轉換元件。  
  
 **另請參閱：**  
  
 ODBC 目的地  
  
 ODBC 目的地編輯器 (連線管理員頁面)  
  
 ODBC 目的地編輯器 (錯誤輸出頁面)  
  
## <a name="operating-scenarios"></a>作業案例  
 本節描述 ODBC 來源和目的地元件的一些主要用途。  
  
### <a name="bulk-copy-data-from-sql-server-tables-to-any-odbc-supported-database-table"></a>從 SQL Server 資料表大量複製資料至任何 ODBC 支援的資料庫資料表  
 您可以使用這些元件，從一或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表大量複製資料至單一 ODBC 支援的資料庫資料表。  
  
 下列範例示範如何建立 SSIS 資料流程工作，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表擷取資料並將資料載入 DB2 資料表。  
  
-   在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中，建立 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]專案。  
  
-   建立 OLE DB 連線管理員，連接到包含要複製之資料的來源 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
-   建立 ODBC 連線管理員，其使用本機安裝的 DB2 ODBC 驅動程式，以及指向本機或遠端 DB2 資料庫的 DSN。 此資料庫是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫資料載入的目的地資料庫。  
  
-   將 OLE DB 來源拖曳到設計介面，然後設定來源從含有要擷取之資料的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫和資料表取得資料。 使用先前建立的 OLE DB 連線管理員。  
  
-   將 ODBC 目的地拖曳到設計介面，將來源輸出連接到 ODBC 目的地，然後設定目的地將資料載入含有從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫擷取之資料的 DB2 資料表。 使用先前建立的 ODBC 連線管理員。  
  
### <a name="bulk-copy-data-from-odbc-supported-database-tables-to-any-sql-server-table"></a>從 ODBC 支援的資料庫資料表大量複製資料至任何 SQL Server 資料表  
 您可以使用這些元件，從一個或多個 ODBC 支援的資料庫資料表大量複製資料至單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫資料表。  
  
 下列範例示範如何建立 SSIS 資料流程工作，從 Sybase 資料庫資料表擷取資料並將資料載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫資料表。  
  
-   在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中開啟新的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
-   建立 ODBC 連線管理員，其使用本機安裝的 Sybase ODBC 驅動程式，以及指向本機或遠端 Sybase 資料庫的 DSN。 此資料庫是擷取資料的來源資料庫。  
  
-   建立 OLE DB 連線管理員，連接到要載入資料的目的地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
-   將 ODBC 來源拖曳到設計介面，然後設定來源從含有要複製之資料的 Sybase 資料表取得資料。 使用先前建立的 ODBC 連線管理員。  
  
-   將 OLE DB 目的地拖曳到設計介面，將來源輸出連接到 OLE DB 目的地，然後設定目的地將資料載入含有從 Sybase 資料庫擷取之資料的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 使用先前建立的 OLE DB 連線管理員。  
  
## <a name="supported-data-types"></a>支援的資料類型  
 ODBC 大量 SSIS 元件支援所有內建 ODBC 資料類型，包括支援大型物件 (CLOB 和 BLOB)。  
  
如 ODBC 3.8 規格中所述，對可延伸 C 類型不提供資料類型支援。下表描述每個 ODBC SQL 類型所用的 SSIS 資料類型。 SSIS 開發人員可以覆寫預設對應，為輸入/輸出資料行指定不同的 SSIS 資料類型，而不影響必要資料轉換的效能。  
  
|ODBC SQL 類型|SSIS 資料類型|註解|  
|-----------------|------------------|------------|  
|SQL_BIT|DT_BOOL||  
|SQL_TINYINT|DT_I1<br /><br />DT_UI1|如果 ODBC 驅動程式將 SQL 資料類型的 UNSIGNED_ATTRIBUTE 設為 SQL_TRUE，該 SQL 資料類型會對應至 SSIS 不帶正負號的類型 (DT_UI1、DT_UI2、DT_UI4、DT_UI8)。|  
|SQL_SMALLINT|DT_I2<br /><br />DT_UI2|如果 ODBC 驅動程式將 SQL 資料類型的 UNSIGNED_ATTRIBUTE 設為 SQL_TRUE，該 SQL 資料類型會對應至 SSIS 不帶正負號的類型 (DT_UI1、DT_UI2、DT_UI4、DT_UI8)。|  
|SQL_INTEGER|DT_I4<br /><br />DTUI4|如果 ODBC 驅動程式將 SQL 資料類型的 UNSIGNED_ATTRIBUTE 設為 SQL_TRUE，該 SQL 資料類型會對應至 SSIS 不帶正負號的類型 (DT_UI1、DT_UI2、DT_UI4、DT_UI8)。|  
|SQL_BIGINT|DT_I8<br /><br />DT_UI8|如果 ODBC 驅動程式將 SQL 資料類型的 UNSIGNED_ATTRIBUTE 設為 SQL_TRUE，該 SQL 資料類型會對應至 SSIS 不帶正負號的類型 (DT_UI1、DT_UI2、DT_UI4、DT_UI8)。|  
|SQL_DOUBLE|DT_R8|  
|SQL_FLOAT|DT_R8|  
|SQL_REAL|DT_R4|  
|SQL_NUMERIC (p,s)|DT_NUMERIC (p,s)<br /><br />DT_R8<br /><br />DT_CY|數值資料類型會對應至 DT_NUMERIC P 是大於或等於 38 而且 S 大於或等於 0 而且 S 小於或等於 p。當至少下列其中一項條件成立時，數值資料類型會對應至 DT_R8:<br /><br />有效位數大於 38<br /><br />小數位數小於零<br /><br />小數位數大於 38<br /><br />小數位數大於有效位數<br /><br /><br /><br />請注意它宣告為 money 資料類型時，將數值資料類型會對應至 DT_CY。|  
|SQL_DECIMAL (p,s)|DT_NUMERIC (p,s)<br /><br />DT_R8<br /><br />DT_CY|Decimal 資料類型會對應至 DT_NUMERIC P 是大於或等於 38 而且 S 大於或等於 0 而且 S 小於或等於 p。當至少下列其中一項條件成立時，則 decimal 資料類型會對應至 DT_R8:<br /><br />有效位數大於 38<br /><br />小數位數小於零<br /><br />小數位數大於 38<br /><br />小數位數大於有效位數<br /><br />請注意它宣告為 money 資料類型時，則 decimal 資料類型會對應至 DT_CY。|  
|SQL_DATE<br /><br />SQL_TYPE_DATE|DT_DBDATE|  
|SQL_TIME<br /><br />SQL_TYPE_TIME|DT_DBTIME|  
|SQL_TIMESTAMP<br /><br />SQL_TYPE_TIMESTAMP|DT_DBTIMESTAMP<br /><br />DT_DBTIMESTAMP2|如果小數位數大於 3，則 SQL_TIMESTAMP 資料類型會對應至 DT_DBTIMESTAMP2。 在所有其他情況下，它們會對應至 DT_DBTIMESTAMP。|  
|SQL_CHAR<br /><br />SQLVARCHAR|DT_STR<br /><br />DT_WSTR<br /><br />DT_TEXT<br /><br />DT_NTEXT|如果資料行長度小於或等於 8000，而且 **ExposeStringsAsUnicode** 屬性為 false，則會使用 DT_STR。<br /><br />如果資料行長度小於或等於 8000，而且 **ExposeStringsAsUnicode** 屬性為 true，則會使用 DT_WSTR。<br /><br />如果資料行長度大於 8000，而且 **ExposeStringsAsUnicode** 屬性為 false，則會使用 DT_TEXT。<br /><br />如果資料行長度大於 8000，而且 **ExposeStringsAsUnicode** 屬性為 true，則會使用 DT_NTEXT。|  
|SQL_LONGVARCHAR|DT_TEXT<br /><br />DT_NTEXT|如果 **ExposeStringsAsUnicode** 屬性為 true，則會使用 DT_NTEXT。|  
|SQL_WCHAR<br /><br />SQL_WVARCHAR|DT_WSTR<br /><br />DT_NTEXT|如果資料行長度小於或等於 4000，則會使用 DT_WSTR。<br /><br />如果資料行長度大於 4000，則會使用 DT_NTEXT。|  
|SQL_WLONGVARCHAR|DT_NTEXT|  
|SQL_BINARY|DT_BYTE<br /><br />DT_IMAGE|如果資料行長度小於或等於 8000，則會使用 DT_BYTES。<br /><br />如果資料行長度大於 8000，則會使用 DT_IMAGE。|  
|SQL_LONGVARBINARY|DT_IMAGE|  
|SQL_GUID|DT_GUID|  
|SQL_INTERVAL_YEAR<br /><br />SQL_INTERVAL_MONTH<br /><br />SQL_INTERVAL_DAY<br /><br />SQL_INTERVAL_HOUR<br /><br />SQL_INTERVAL_MINUTE<br /><br />SQL_INTERVAL_SECOND<br /><br />SQL_INTERVAL_YEAR_TO_MONTH<br /><br />SQL_INTERVAL_DAY_TO_HOUR<br /><br />SQL_INTERVAL_DAY_TO_MINUTE<br /><br />SQL_INTERVAL_DAY_TO_SECOND<br /><br />SQL_INTERVAL_HOUR_TO_MINUTE<br /><br />SQL_INTERVAL_HOUR_TO_SECOND<br /><br />SQL_INTERVAL_MINUTE_TO_SECOND|DT_WSTR|  
|提供者特定的資料類型|DT_BYTES<br /><br />DT_IMAGE|如果資料行長度小於或等於 8000，則會使用 DT_BYTES。<br /><br />如果資料行長度為零或大於 8000，則會使用 DT_IMAGE。|  
  
## <a name="in-this-section"></a>本節內容  
  
-   [ODBC 來源](odbc-source.md)  
  
-   [ODBC 目的地](odbc-destination.md)  
  
 
