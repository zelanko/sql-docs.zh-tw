---
description: bcp_setcolfmt
title: bcp_setcolfmt |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_setcolfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_setcolfmt function
ms.assetid: afb47987-39e7-4079-ad66-e0abf4d4c72b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 01576468fb54618e34f72bbd42fbd1ae861c8520
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420532"
---
# <a name="bcp_setcolfmt"></a>bcp_setcolfmt
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **Bcp_setcolfmt**函數會取代[bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)。 在指定資料行定序時，必須使用 **bcp_setcolfmt** 函數。 [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md) 可以用來指定一個以上的資料行格式。  
  
 此函數會提供彈性的方法來指定大量複製作業中的資料行格式。 它會用來設定個別的資料行格式屬性。 **Bcp_setcolfmt**的每個呼叫都會設定一個資料行格式屬性。  
  
 **Bcp_setcolfmt**函數會指定使用者檔案中資料的來源或目標格式。 當做來源格式使用時， **bcp_setcolfmt** 會將現有資料檔案的格式指定為大量複製中的資料來源，以供中的資料表使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 當做目標格式使用時，會使用以 **bcp_setcolfmt**指定的資料行格式建立資料檔案。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_setcolfmt (  
        HDBC hdbc,  
        INT field,  
        INT property,  
        void* pValue,  
        INT cbValue);  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *領域*  
 這是要設定屬性的序數資料行編號。  
  
 *property*  
 這是其中一個屬性常數。 屬性常數會在這個資料表中定義。  
  
|屬性|值|描述|  
|--------------|-----------|-----------------|  
|BCP_FMT_TYPE|BYTE|這是使用者檔案中，此資料行的資料類型。 如果與資料庫資料表中，對應資料行的資料類型不同，大量複製就會轉換資料 (如果可能的話)。<br /><br /> BCP_FMT_TYPE 參數是透過 sqlncli.h 中的 SQL Server 資料類型 Token，而非透過 ODBC C 資料類型列舉值列舉。 例如，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專屬類型 SQLCHARACTER 來指定字元字串 ODBC type SQL_C_CHAR。<br /><br /> 若要指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的預設資料表示法，將此參數設定為 0。<br /><br /> 針對從 SQL Server 大量複製到檔案中，當 BCP_FMT_TYPE 是 SQLDECIMAL 或 SQLNUMERIC 時，如果來源資料行不是 decimal 或 numeric，則會使用預設的精確度和小**數位****數**。 否則，如果來源資料行是 **decimal** 或 **numeric**，則會使用來源資料行的精確度和小數位數。|  
|BCP_FMT_INDICATOR_LEN|INT|這是指標 (前置詞) 的位元組長度。<br /><br /> 這是資料行資料內，長度/null 指標的長度 (以位元組為單位)。 有效的指標長度值為 0 (不使用指標時)、1、2 或 4。<br /><br /> 若要指定預設大量複製指標使用率，將此參數設定為 SQL_VARLEN_DATA。<br /><br /> 這些指標會出現在任何資料正前方的記憶體中，以及所套用之資料正前方的資料檔案中。<br /><br /> 如果使用多種指定資料檔案資料行長度的方式 (例如指標和最大資料行長度，或指標和結束字元順序)，大量複製會選擇導致複製最少量資料的方式。<br /><br /> 大量複製在不透過使用者操作來調整資料格式時所產生的資料檔案，會在資料行資料長度可以改變，或資料行可以當做值接受 NULL 時包含指標。|  
|BCP_FMT_DATA_LEN|DBINT|這是資料的位元組長度 (資料行長度)<br /><br /> 這是使用者檔案中此資料行之資料的最大長度 (以位元組為單位)，不包括任何長度指標或結束字元的長度。<br /><br /> 將 BCP_FMT_DATA_LEN 設定為 BCP_FMT_DATA 表示資料檔案資料行中的所有值都會 (或應該) 設定為 NULL。<br /><br /> 將 BCP_FMT_DATA_LEN 設定為 SQL_VARLEN_DATA 表示系統應該決定每個資料行中的資料長度。 對於某些資料行，這可能表示長度/null 指標會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複本之資料前產生，或者表示該指標應該會在複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料中出現。<br /><br /> 對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 字元和二進位資料類型，BCP_FMT_DATA_LEN 可能是 SQL_VARLEN_DATA、SQL_NULL_DATA、0 或某個正值。 如果 BCP_FMT_DATA_LEN 為 SQL_VARLEN_DATA，系統會使用長度指標 (如果存在) 或結束字元順序來決定資料的長度。 如果同時提供長度指標與結束字元順序，大量複製會使用導致複製最少量資料者。 如果 BCP_FMT_DATA_LEN 為 SQL_VARLEN_DATA，資料類型為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 字元或二進位類型，而且長度指標和結束字元順序都未指定，系統會傳回錯誤訊息。<br /><br /> 如果 BCP_FMT_DATA_LEN 為 0 或正值，則系統會使用 BCP_FMT_DATA_LEN 當做資料長度的最大值。 不過，如果除了正數的 BCP_FMT_DATA_LEN 之外，也提供長度指標或結束字元順序，系統會使用導致複製最少量資料的方法來決定資料長度。<br /><br /> BCP_FMT_DATA_LEN 值表示資料的位元組計數。 如果字元資料是以 Unicode 寬字元表示，則 BCP_FMT_DATA_LEN 正參數值表示字元數乘以每個字元的大小 (以位元組為單位)。|  
|BCP_FMT_TERMINATOR|LPCBYTE|用於此資料行之結束字元順序的指標 (ANSI 或 Unicode 中較適合者)。 此參數主要用於字元資料類型，因為其他所有類型都屬固定長度；如果是二進位資料，則需要一個長度指標，才能正確記錄出現的位元組數目。<br /><br /> 為避免結束已擷取的資料，或要指出使用者檔案中的資料未結束，將此參數設定為 NULL。<br /><br /> 如果使用多種指定使用者檔案資料行長度的方式 (例如結束字元和長度指標，或結束字元和資料行長度最大值)，大量複製會選擇導致複製最少量資料的方式。<br /><br /> 大量複製 API 會視需要執行 Unicode 到 MBCS 的字元轉換。 請務必確認結束字元位元組字串與位元組字串長度的設定正確。|  
|BCP_FMT_SERVER_COL|INT|資料行在資料庫中的序數位置。|  
|BCP_FMT_COLLATION|LPCSTR|定序名稱。|  
  
 *pValue*  
 這是要與 *屬性*相關聯之值的指標。 它允許每個資料行格式屬性個別設定。  
  
 *cbvalue*  
 這是屬性緩衝區的長度 (以位元組為單位)。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 此函數會取代 **bcp_colfmt** 函式。 **Bcp_colfmt**的所有功能都是在**bcp_setcolfmt**函數中提供。 此外，也提供資料行定序的支援。 建議使用以下提供的順序設定下列資料行格式屬性：  
  
 BCP_FMT_SERVER_COL  
  
 BCP_FMT_DATA_LEN  
  
 BCP_FMT_TYPE  
  
 **Bcp_setcolfmt**函數可讓您指定大量複製的使用者檔案格式。 針對大量複製，格式包含下列部分：  
  
-   從使用者檔案資料行對應至資料庫資料行。  
  
-   每個使用者檔案資料行的資料類型。  
  
-   每個資料行的選擇性指標長度。  
  
-   每個使用者檔案資料行的資料最大長度。  
  
-   每個資料行的選擇性結束位元組順序。  
  
-   選擇性結束位元組順序的長度。  
  
 **Bcp_setcolfmt**的每個呼叫都會指定一個使用者檔案資料行的格式。 例如，若要在五個數據行的使用者資料檔案中變更三個數據行的預設值，請先呼叫[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) ** (5) **，然後呼叫**bcp_setcolfmt**五次，其中三次呼叫會設定您的自訂格式。 針對剩餘的兩個呼叫，將 BCP_FMT_TYPE 設定為0，並將 BCP_FMT_INDICATOR_LENGTH、BCP_FMT_DATA_LEN 和 *cbValue* 分別設定為0、SQL_VARLEN_DATA 和0。 此程序會複製全部五個資料行，其中三個為您自訂的格式，而另兩個為預設格式。  
  
 呼叫**bcp_setcolfmt**之前，必須先呼叫**bcp_columns**函數。  
  
 您必須針對使用者檔案中每個資料行的每個屬性呼叫 **bcp_setcolfmt** 一次。  
  
 您不需要將使用者檔案中的所有資料複製到 SQL Server 資料表。 若要略過資料行，請指定資料行的資料格式，並將 BCP_FMT_SERVER_COL 參數設定為 0。 如果您要略過資料行，則必須指定其類型。  
  
 [Bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)函數可以用來保存格式規格。  
  
## <a name="bcp_setcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_setcolfmt 對於增強型日期和時間功能的支援  
 使用日期/時間類型的 BCP_FMT_TYPE 屬性所使用的型別，就像是 [增強型日期和時間類型的大量複製變更中所指定的類型 &#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 如需詳細資訊，請參閱 [&#40;ODBC&#41;的日期和時間改進 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
