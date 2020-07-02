---
title: bcp_colfmt |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_colfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_colfmt function
ms.assetid: 5c3b6299-80c7-4e84-8e69-4ff33009548e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9bebe50f7a31168455d21c45aa28cc7c0efa796e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783452"
---
# <a name="bcp_colfmt"></a>bcp_colfmt
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  在使用者檔案中指定資料的來源或目標格式。 當做來源格式使用時， **bcp_colfmt**會將當做大量複製中資料來源使用之現有資料檔案的格式指定為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 當做目標格式使用時，會使用以**bcp_colfmt**指定的資料行格式建立資料檔案。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_colfmt (  
        HDBC hdbc,  
        INT idxUserDataCol,  
        BYTE eUserDataType,  
        INT cbIndicator,  
        DBINT cbUserData,  
        LPCBYTE pUserDataTerm,  
        INT cbUserDataTerm,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *idxUserDataCol*  
 這是使用者資料檔案中，要指定其格式的序數資料行編號。 第一個資料行是 1。  
  
 *eUserDataType*  
 這是使用者檔案中，此資料行的資料類型。 如果與資料庫資料表（*idxServerColumn*）中對應資料行的資料類型不同，大量複製就會轉換資料（如果可能的話）。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]在*eUserDataType*參數中引進了 SQLXML 和 SQLUDT 資料類型標記的支援。  
  
 *EUserDataType*參數是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sqlncli 中的資料類型標記所列舉，而不是 ODBC C 資料類型枚舉器。 例如，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專屬類型 SQLCHARACTER 來指定字元字串 ODBC type SQL_C_CHAR。  
  
 若要指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的預設資料表示法，將此參數設定為 0。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當*EUSERDATATYPE*為 SQLDECIMAL 或 SQLNUMERIC 時，將大量複製到檔案中：  
  
-   如果來源資料行不是**decimal**或**numeric**，就會使用預設的有效位數和小數位數。  
  
-   如果來源資料行是**小數**或**數值**，則會使用來源資料行的有效位數和小數位數。  
  
 *cbIndicator*  
 這是資料行資料內，長度/null 指標的長度 (以位元組為單位)。 有效的指標長度值為 0 (不使用指標時)、1、2、4 或 8。  
  
 若要指定預設大量複製指標使用率，將此參數設定為 SQL_VARLEN_DATA。  
  
 這些指標會出現在任何資料正前方的記憶體中，以及所套用之資料正前方的資料檔案中。  
  
 如果使用多種指定資料檔案資料行長度的方式 (例如指標和最大資料行長度，或指標和結束字元順序)，大量複製會選擇導致複製最少量資料的方式。  
  
 大量複製在不透過使用者操作來調整資料格式時所產生的資料檔案，會在資料行資料長度可以改變，或資料行可以當做值接受 NULL 時包含指標。  
  
 *cbUserData*  
 這是使用者檔案中此資料行之資料的最大長度 (以位元組為單位)，不包括任何長度指標或結束字元的長度。  
  
 將*cbUserData*設定為 SQL_Null_DATA 表示資料檔案欄位中的所有值都是，或應設定為 Null。  
  
 將*cbUserData*設定為 SQL_VARLEN_DATA 表示系統應該決定每個資料行中的資料長度。 對於某些資料行，這可能表示長度/null 指標會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複本之資料前產生，或者表示該指標應該會在複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料中出現。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是字元和二進位資料類型， *cbUserData*可以是 SQL_VARLEN_DATA、SQL_Null_DATA、0或某個正數值。 如果*cbUserData*為 SQL_VARLEN_DATA，則系統會使用長度指標（如果有的話）或結束字元序列來決定資料的長度。 如果同時提供長度指標與結束字元順序，大量複製會使用導致複製最少量資料者。 如果*cbUserData*為 SQL_VARLEN_DATA，則資料類型為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 字元或二進位類型，而且長度指標和結束字元順序都未指定，系統會傳回錯誤訊息。  
  
 如果 *cbUserData* 為 0 或正值，則系統會使用 *cbUserData* 當作最大的資料長度。 不過，如果除了正的 *cbUserData* 之外，也提供長度指標或結束字元順序，系統會使用導致複製最少量資料的方式決定資料長度。  
  
 *cbUserData* 值表示資料的位元組計數。 如果字元資料是以 Unicode 寬字元表示，則 *cbUserData* 正參數值表示字元數乘以每個字元的大小 (以位元組為單位)。  
  
 *pUserDataTerm*  
 這是要用於此資料行的結束字元順序。 此參數主要用於字元資料類型，因為其他所有類型都屬固定長度；如果是二進位資料，則需要一個長度指標，才能正確記錄出現的位元組數目。  
  
 為避免結束已擷取的資料，或要指出使用者檔案中的資料未結束，將此參數設定為 NULL。  
  
 如果使用多種指定使用者檔案資料行長度的方式 (例如結束字元和長度指標，或結束字元和資料行長度最大值)，大量複製會選擇導致複製最少量資料的方式。  
  
 大量複製 API 會視需要執行 Unicode 到 MBCS 的字元轉換。 請務必確認結束字元位元組字串與位元組字串長度的設定正確。  
  
 *cbUserDataTerm*  
 這是要用於此資料行的結束字元順序長度 (以位元組為單位)。 如果資料中沒有或不需要結束字元，將此值設定為 0。  
  
 *idxServerCol*  
 這是資料行在資料庫資料表中的序數位置。 第一個資料行編號為 1。 資料行的序數位置是由[SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)所報告。  
  
 如果此值為 0，大量複製在資料檔案中會忽略資料行。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 **Bcp_colfmt**函數可讓您指定大量複製的使用者檔案格式。 針對大量複製，格式包含下列部分：  
  
-   從使用者檔案資料行對應至資料庫資料行。  
  
-   每個使用者檔案資料行的資料類型。  
  
-   每個資料行的選擇性指標長度。  
  
-   每個使用者檔案資料行的資料最大長度。  
  
-   每個資料行的選擇性結束位元組順序。  
  
-   選擇性結束位元組順序的長度。  
  
 **Bcp_colfmt**的每個呼叫都會指定一個使用者檔案資料行的格式。 例如，若要在五個數據行的使用者資料檔案中變更三個數據行的預設設定，請先呼叫[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)**（5）**，然後呼叫**bcp_colfmt**五次，其中三個呼叫會設定您的自訂格式。 針對剩餘的兩個呼叫，請將*eUserDataType*設定為0，並分別將*cbIndicator*、 *cbUserData*和*cbUserDataTerm*設定為0、SQL_VARLEN_DATA 和0。 此程序會複製全部五個資料行，其中三個為您自訂的格式，而另兩個為預設格式。  
  
 若為*cbIndicator*，值為8表示大數數值型別現在有效。 如果有針對其對應資料行是新最大類型的欄位指定前置詞，則僅能將該前置詞設定為 8。 如需詳細資訊，請參閱[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)。  
  
 呼叫**bcp_colfmt**之前，必須先呼叫**bcp_columns**函式。  
  
 您必須針對使用者檔案中的每個資料行呼叫一次**bcp_colfmt** 。  
  
 針對任何使用者檔案資料行多次呼叫**bcp_colfmt**會造成錯誤。  
  
 您不需要將使用者檔案中的所有資料複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 若要略過資料行，請將*並將 idxservercol*參數設定為0，以指定資料行的資料格式。 如果您要略過資料行，則必須指定其類型。  
  
 [Bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)函數可以用來保存格式規格。  
  
## <a name="bcp_colfmt-support-for-enhanced-date-and-time-features"></a>bcp_colfmt 支援增強的日期和時間功能  
 如需有關與日期/時間類型的*eUserDataType*參數搭配使用之類型的詳細資訊，請參閱[增強型日期和時間類型的大量複製變更 &#40;OLE DB 和 ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
