---
title: bcp_setcolfmt |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_setcolfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_setcolfmt function
ms.assetid: afb47987-39e7-4079-ad66-e0abf4d4c72b
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 87c86d900f8923bfbed16fc890298d49be036909
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033643"
---
# <a name="bcpsetcolfmt"></a>bcp_setcolfmt
  **Bcp_setcolfmt**函數會取代[bcp_colfmt](bcp-colfmt.md)。 在指定資料行定序**bcp_setcolfmt**函式必須使用。 [bcp_setbulkmode](bcp-setbulkmode.md)可以用來指定多個資料行格式。  
  
 此函數會提供彈性的方法來指定大量複製作業中的資料行格式。 它會用來設定個別的資料行格式屬性。 每次呼叫**bcp_setcolfmt**設定一個資料行格式屬性。  
  
 **Bcp_setcolfmt**函式指定使用者檔案中的資料來源或目標格式。 當做來源格式使用時**bcp_setcolfmt**指定現有的資料檔案做為資料來源中的資料表中大量複製資料的格式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 資料檔案當做目標格式使用時，會建立使用指定的資料行格式**bcp_setcolfmt**。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_setcolfmt (  
HDBC   
hdbc  
,  
INT   
field  
,  
INT   
property  
,  
void*   
pValue  
,  
INT   
cbValue  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *field*  
 這是要設定屬性的序數資料行編號。  
  
 *property*  
 這是其中一個屬性常數。 屬性常數會在這個資料表中定義。  
  
|屬性|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|BCP_FMT_TYPE|BYTE|這是使用者檔案中，此資料行的資料類型。 如果與資料庫資料表中，對應資料行的資料類型不同，大量複製就會轉換資料 (如果可能的話)。<br /><br /> BCP_FMT_TYPE 參數是透過 sqlncli.h 中的 SQL Server 資料類型 Token，而非透過 ODBC C 資料類型列舉值列舉。 例如，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專屬類型 SQLCHARACTER 來指定字元字串 ODBC type SQL_C_CHAR。<br /><br /> 若要指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的預設資料表示法，將此參數設定為 0。<br /><br /> 若要從 SQL Server 大量複製到檔案，當 BCP_FMT_TYPE 為 SQLDECIMAL 或 SQLNUMERIC 時：<br /><br /> -如果來源資料行不是**十進位**或**數值**，會使用預設有效位數和小數位數。<br />-如果來源資料行是**十進位**或**數值**，使用的有效位數和小數位數的來源資料行。|  
|BCP_FMT_INDICATOR_LEN|INT|這是指標 (前置詞) 的位元組長度。<br /><br /> 這是資料行資料內，長度/null 指標的長度 (以位元組為單位)。 有效的指標長度值為 0 (不使用指標時)、1、2 或 4。<br /><br /> 若要指定預設大量複製指標使用率，將此參數設定為 SQL_VARLEN_DATA。<br /><br /> 這些指標會出現在任何資料正前方的記憶體中，以及所套用之資料正前方的資料檔案中。<br /><br /> 如果使用多種指定資料檔案資料行長度的方式 (例如指標和最大資料行長度，或指標和結束字元順序)，大量複製會選擇導致複製最少量資料的方式。<br /><br /> 大量複製在不透過使用者操作來調整資料格式時所產生的資料檔案，會在資料行資料長度可以改變，或資料行可以當做值接受 NULL 時包含指標。|  
|BCP_FMT_DATA_LEN|DBINT|這是資料的位元組長度 (資料行長度)<br /><br /> 這是使用者檔案中此資料行之資料的最大長度 (以位元組為單位)，不包括任何長度指標或結束字元的長度。<br /><br /> 將 BCP_FMT_DATA_LEN 設定為 BCP_FMT_DATA 表示資料檔案資料行中的所有值都會 (或應該) 設定為 NULL。<br /><br /> 將 BCP_FMT_DATA_LEN 設定為 SQL_VARLEN_DATA 表示系統應該決定每個資料行中的資料長度。 對於某些資料行，這可能表示長度/null 指標會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複本之資料前產生，或者表示該指標應該會在複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料中出現。<br /><br /> 對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 字元和二進位資料類型，BCP_FMT_DATA_LEN 可能是 SQL_VARLEN_DATA、SQL_NULL_DATA、0 或某個正值。 如果 BCP_FMT_DATA_LEN 為 SQL_VARLEN_DATA，系統會使用長度指標 (如果存在) 或結束字元順序來決定資料的長度。 如果同時提供長度指標與結束字元順序，大量複製會使用導致複製最少量資料者。 如果 BCP_FMT_DATA_LEN 為 SQL_VARLEN_DATA，資料類型為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 字元或二進位類型，而且長度指標和結束字元順序都未指定，系統會傳回錯誤訊息。<br /><br /> 如果 BCP_FMT_DATA_LEN 為 0 或正值，則系統會使用 BCP_FMT_DATA_LEN 當做資料長度的最大值。 不過，如果除了正數的 BCP_FMT_DATA_LEN 之外，也提供長度指標或結束字元順序，系統會使用導致複製最少量資料的方法來決定資料長度。<br /><br /> BCP_FMT_DATA_LEN 值表示資料的位元組計數。 如果字元資料是以 Unicode 寬字元表示，則 BCP_FMT_DATA_LEN 正參數值表示字元數乘以每個字元的大小 (以位元組為單位)。|  
|BCP_FMT_TERMINATOR|LPCBYTE|用於此資料行之結束字元順序的指標 (ANSI 或 Unicode 中較適合者)。 此參數主要用於字元資料類型，因為其他所有類型都屬固定長度；如果是二進位資料，則需要一個長度指標，才能正確記錄出現的位元組數目。<br /><br /> 為避免結束已擷取的資料，或要指出使用者檔案中的資料未結束，將此參數設定為 NULL。<br /><br /> 如果使用多種指定使用者檔案資料行長度的方式 (例如結束字元和長度指標，或結束字元和資料行長度最大值)，大量複製會選擇導致複製最少量資料的方式。<br /><br /> 大量複製 API 會視需要執行 Unicode 到 MBCS 的字元轉換。 請務必確認結束字元位元組字串與位元組字串長度的設定正確。|  
|BCP_FMT_SERVER_COL|INT|資料行在資料庫中的序數位置。|  
|BCP_FMT_COLLATION|LPCSTR|定序名稱。|  
  
 *pValue*  
 若要建立關聯之值的指標*屬性*。 它允許每個資料行格式屬性個別設定。  
  
 *cbvalue*  
 這是屬性緩衝區的長度 (以位元組為單位)。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 這個函數會取代**bcp_colfmt**函式。 所有功能**bcp_colfmt**中提供**bcp_setcolfmt**函式。 此外，也提供資料行定序的支援。 建議使用以下提供的順序設定下列資料行格式屬性：  
  
 BCP_FMT_SERVER_COL  
  
 BCP_FMT_DATA_LEN  
  
 BCP_FMT_TYPE  
  
 **Bcp_setcolfmt**函式可讓您指定大量複製的使用者檔案格式。 針對大量複製，格式包含下列部分：  
  
-   從使用者檔案資料行對應至資料庫資料行。  
  
-   每個使用者檔案資料行的資料類型。  
  
-   每個資料行的選擇性指標長度。  
  
-   每個使用者檔案資料行的資料最大長度。  
  
-   每個資料行的選擇性結束位元組順序。  
  
-   選擇性結束位元組順序的長度。  
  
 每次呼叫**bcp_setcolfmt**指定一個使用者檔案資料行的格式。 例如，若要變更在五個資料行的使用者資料檔案中的三個資料行的預設設定，請先呼叫[bcp_columns](bcp-columns.md)**(5)**，然後呼叫**bcp_setcolfmt**五次，使用三個呼叫會設定您的自訂格式。 對於其餘的兩個呼叫，將 BCP_FMT_TYPE 設定為 0，而設定 BCP_FMT_INDICATOR_LENGTH、 BCP_FMT_DATA_LEN 和*cbValue*為 0、 SQL_VARLEN_DATA 和 0 分別。 此程序會複製全部五個資料行，其中三個為您自訂的格式，而另兩個為預設格式。  
  
 **Bcp_columns**函式必須呼叫之前先呼叫**bcp_setcolfmt**。  
  
 您必須呼叫**bcp_setcolfmt**使用者檔案中的每個資料行的每個屬性一次。  
  
 您不需要將使用者檔案中的所有資料複製到 SQL Server 資料表。 若要略過資料行，請指定資料行的資料格式，並將 BCP_FMT_SERVER_COL 參數設定為 0。 如果您要略過資料行，則必須指定其類型。  
  
 [Bcp_writefmt](bcp-writefmt.md)函式可以用來保存格式規格。  
  
## <a name="bcpsetcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_setcolfmt 對於增強型日期和時間功能的支援  
 搭配日期/時間類型之 BCP_FMT_TYPE 屬性類型為當做中所指定[增強型日期和時間類型的大量複製變更&#40;OLE DB 和 ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 如需詳細資訊，請參閱[日期和時間增強功能&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  