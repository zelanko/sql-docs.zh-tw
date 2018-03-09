---
title: bcp_colfmt | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- bcp_colfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_colfmt function
ms.assetid: 5c3b6299-80c7-4e84-8e69-4ff33009548e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c19dd268f958bc35f6e41fd6a6283ca23beb60e9
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="bcpcolfmt"></a>bcp_colfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在使用者檔案中指定資料的來源或目標格式。 當做來源格式使用時**bcp_colfmt**指定現有的資料檔案做為大量複製中的資料來源的格式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。 資料檔案當做目標格式使用時，會建立使用指定的資料行格式**bcp_colfmt**。  
  
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
 這是使用者檔案中，此資料行的資料類型。 如果不同於資料庫資料表中的對應資料行的資料類型 (*idxServerColumn*)，大量複製會盡可能將資料轉換。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]導入 SQLXML 和 SQLUDT 資料類型 token 中的支援*eUserDataType*參數。  
  
 *EUserDataType*參數會列舉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sqlncli.h 中的資料類型 token、 不 ODBC C 資料類型列舉值。 例如，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專屬類型 SQLCHARACTER 來指定字元字串 ODBC type SQL_C_CHAR。  
  
 若要指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的預設資料表示法，將此參數設定為 0。  
  
 的大量複製出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到檔案中，當*eUserDataType*為 SQLDECIMAL 或 sqlnumeric 時：  
  
-   如果來源資料行不是**十進位**或**數值**，會使用預設有效位數和小數位數。  
  
-   如果來源資料行是**十進位**或**數值**，使用的有效位數和小數位數的來源資料行。  
  
 *cbIndicator*  
 這是資料行資料內，長度/null 指標的長度 (以位元組為單位)。 有效的指標長度值為 0 (不使用指標時)、1、2、4 或 8。  
  
 若要指定預設大量複製指標使用率，將此參數設定為 SQL_VARLEN_DATA。  
  
 這些指標會出現在任何資料正前方的記憶體中，以及所套用之資料正前方的資料檔案中。  
  
 如果使用多種指定資料檔案資料行長度的方式 (例如指標和最大資料行長度，或指標和結束字元順序)，大量複製會選擇導致複製最少量資料的方式。  
  
 大量複製在不透過使用者操作來調整資料格式時所產生的資料檔案，會在資料行資料長度可以改變，或資料行可以當做值接受 NULL 時包含指標。  
  
 *cbUserData*  
 這是使用者檔案中此資料行之資料的最大長度 (以位元組為單位)，不包括任何長度指標或結束字元的長度。  
  
 設定*cbUserData*為 SQL_NULL_DATA 表示資料檔案資料行中的所有值，或應該設定為 NULL。  
  
 設定*cbUserData*為 SQL_VARLEN_DATA 表示系統應該決定每個資料行中的資料長度。 對於某些資料行，這可能表示長度/null 指標會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複本之資料前產生，或者表示該指標應該會在複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料中出現。  
  
 如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字元和二進位資料類型， *cbUserData*可以是 SQL_VARLEN_DATA、 SQL_NULL_DATA、 0 或某個正數值。 如果*cbUserData*為 SQL_VARLEN_DATA，系統會使用長度指標，如果存在或結束字元順序來決定資料長度。 如果同時提供長度指標與結束字元順序，大量複製會使用導致複製最少量資料者。 如果*cbUserData*為 SQL_VARLEN_DATA，資料類型是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字元或二進位類型，以及長度指標和結束字元順序都未指定，系統會傳回錯誤訊息。  
  
 如果*cbUserData*為 0 或正值，系統會使用*cbUserData*為最大資料長度。 不過，如果除了正*cbUserData*提供長度指標或結束字元順序，系統會決定資料長度的方法來產生最少的資料會被複製。  
  
 *CbUserData*值表示資料的位元組計數。 如果字元資料以 Unicode 寬字元，則正值表示*cbUserData*參數值表示乘以大小，以位元組為單位，每個字元的字元數。  
  
 *pUserDataTerm*  
 這是要用於此資料行的結束字元順序。 此參數主要用於字元資料類型，因為其他所有類型都屬固定長度；如果是二進位資料，則需要一個長度指標，才能正確記錄出現的位元組數目。  
  
 為避免結束已擷取的資料，或要指出使用者檔案中的資料未結束，將此參數設定為 NULL。  
  
 如果使用多種指定使用者檔案資料行長度的方式 (例如結束字元和長度指標，或結束字元和資料行長度最大值)，大量複製會選擇導致複製最少量資料的方式。  
  
 大量複製 API 會視需要執行 Unicode 到 MBCS 的字元轉換。 請務必確認結束字元位元組字串與位元組字串長度的設定正確。  
  
 *cbUserDataTerm*  
 這是要用於此資料行的結束字元順序長度 (以位元組為單位)。 如果資料中沒有或不需要結束字元，將此值設定為 0。  
  
 *idxServerCol*  
 這是資料行在資料庫資料表中的序數位置。 第一個資料行編號為 1。 資料行的序數位置由報告[SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)。  
  
 如果此值為 0，大量複製在資料檔案中會忽略資料行。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 **Bcp_colfmt**函式可讓您指定大量複製的使用者檔案格式。 針對大量複製，格式包含下列部分：  
  
-   從使用者檔案資料行對應至資料庫資料行。  
  
-   每個使用者檔案資料行的資料類型。  
  
-   每個資料行的選擇性指標長度。  
  
-   每個使用者檔案資料行的資料最大長度。  
  
-   每個資料行的選擇性結束位元組順序。  
  
-   選擇性結束位元組順序的長度。  
  
 每次呼叫**bcp_colfmt**指定一個使用者檔案資料行的格式。 例如，若要變更在五個資料行的使用者資料檔案中的三個資料行的預設設定，請先呼叫[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)**(5)**，然後呼叫**bcp_colfmt**五次，其中三個呼叫會設定您的自訂格式。 針對其餘的兩個呼叫中，設定*eUserDataType*為 0，並設定*cbIndicator*， *cbUserData*，和*cbUserDataTerm*為 0，SQL_VARLEN資料 （_d)，和 0 分別。 此程序會複製全部五個資料行，其中三個為您自訂的格式，而另兩個為預設格式。  
  
 如*cbIndicator*，8 表示大數值類型的值現在就有效。 如果有針對其對應資料行是新最大類型的欄位指定前置詞，則僅能將該前置詞設定為 8。 如需詳細資訊，請參閱[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)。  
  
 **Bcp_columns**函式必須呼叫任何呼叫之前**bcp_colfmt**。  
  
 您必須呼叫**bcp_colfmt**一次是針對使用者檔案中的每個資料行。  
  
 呼叫**bcp_colfmt**一次以上的任何使用者檔案資料行導致錯誤。  
  
 您不需要將使用者檔案中的所有資料複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 若要略過資料行，指定資料行設定資料的格式*idxServerCol*參數為 0。 如果您要略過資料行，則必須指定其類型。  
  
 [Bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)函式可以用來保存格式規格。  
  
## <a name="bcpcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_colfmt 支援增強的日期和時間功能  
 如需有關搭配使用的型別資訊*eUserDataType*參數的日期/時間類型，請參閱[增強型日期和時間類型 &#40; OLE DB 和 ODBC &#41; 的大量複製變更](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)。  
  
 如需詳細資訊，請參閱[日期和時間增強功能 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
