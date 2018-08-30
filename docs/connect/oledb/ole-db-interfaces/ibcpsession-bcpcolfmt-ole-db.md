---
title: 'Ibcpsession:: Bcpcolfmt (OLE DB) |Microsoft Docs'
description: IBCPSession::BCPColFmt (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBCPSession::BCPColFmt (OLE DB)
apitype: COM
helpviewer_keywords:
- BCPColFmt method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: dd4b380e0fe16260eb8d8be181b5a110004a1366
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025581"
---
# <a name="ibcpsessionbcpcolfmt-ole-db"></a>IBCPSession::BCPColFmt (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  在程式變數與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料行之間建立繫結。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPColFmt(   
      DBORDINAL idxUserDataCol,  
      int eUserDataType,  
      int cbIndicator,  
      int cbUserData,  
      BYTE *pbUserDataTerm,  
      int cbUserDataTerm,  
      DBORDINAL idxServerCol);  
```  
  
## <a name="remarks"></a>Remarks  
 **BCPColFmt** 方法是用來建立 BCP 資料檔欄位與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料行之間的繫結。 它會使用資料行的長度、類型、結束字元和前置長度當做參數，並為個別欄位設定每一個屬性。  
  
 如果使用者選擇互動模式，就會呼叫這個方法兩次；一次是根據預設值設定資料行格式 (預設值是根據伺服器資料行的類型)，另一次是根據互動模式期間選擇之用戶端的資料行類型，針對每一個資料行設定格式。  
  
 在非互動模式中，每一個資料行只會呼叫這個方法一次，以便將每一個資料行的類型設定為字元或原生類型，或是設定資料行和資料列結束字元。  
  
 **BCPColFmt** 方法可讓您指定大量複製的使用者檔案格式。 針對大量複製，格式包含下列部分：  
  
-   從使用者檔案欄位對應至資料庫資料行。  
  
-   每個使用者檔案欄位的資料類型。  
  
-   每個欄位的選擇性指標長度。  
  
-   每個使用者檔案欄位的資料最大長度。  
  
-   每個欄位的選擇性結束位元組順序。  
  
-   選擇性結束位元組順序的長度。  
  
 **BCPColFmt** 的每個呼叫都會針對一個使用者檔案欄位指定格式。 例如，若要在五個欄位的使用者資料檔案中變更三個欄位的預設值，請先呼叫 `BCPColumns(5)`，然後呼叫 **BCPColFmt** 五次，其中三次呼叫會設定您的自訂格式。 針對其餘的兩個呼叫中，設定*eUserDataType*為 BCP_TYPE_DEFAULT，並將*cbIndicator*， *cbUserData*，和*cbUserDataTerm*至 0、bcp_variable_length 和 0 分別。 此程序會複製全部五個資料行，其中三個為您自訂的格式，而另兩個為預設格式。  
  
> [!NOTE]  
>  必須先呼叫 [IBCPSession::BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md) 方法，才能進行 **BCPColFmt** 的任何呼叫。 您必須在使用者檔案中，針對每個資料行呼叫 **BCPColFmt** 一次。 針對任何使用者檔案資料行多次呼叫 **BCPColFmt** 會產生錯誤。  
  
 您不必將使用者檔案中的所有資料複製到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。 若要略過資料行，請指定資料行的資料格式，並將 idxServerCol 參數設定為 0。 為了略過欄位，您仍然需要所有資訊，才能讓此方法正確運作。  
  
 **注意**：可使用 [IBCPSession::BCPWriteFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) 函式來保存透過 **BCPColFmt** 提供的格式規格。  
  
## <a name="arguments"></a>引數  
 *idxUserDataCol*[in]  
 使用者的資料檔案中的欄位索引。  
  
 *eUserDataType*[in]  
 使用者的資料檔案中欄位的資料類型。 可用的資料類型會列在 OLE DB Driver for SQL Server 標頭檔 (msoledbsql.h)，格式為 BCP_TYPE_XXX，例如 BCP_TYPE_SQLINT4。 如果指定了 BCP_TYPE_DEFAULT 值，提供者會嘗試使用與資料表或檢視表資料行類型相同的類型。 當 **eUserDataType** 引數為 BCP_TYPE_SQLDECIMAL 或 BCP_TYPE_SQLNUMERIC 時，要從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進行大量複製作業，並複製到檔案中：  
  
-   如果來源資料行不是小數或數值，便會使用預設的有效位數和小數位數。  
  
-   如果來源資料行是小數或數值，則會使用來源資料行的有效位數和小數位數。  
  
 *cbIndicator*[in]  
 欄位的前置長度。 預設值為 BCP_PREFIX_DEFAULT。 此前置詞的有效長度為 0、1、2、4 和 8。 前置詞大小 8 最常用來指示此欄位已分成若干區塊。 這可用來有效率地大量複製大型值類型的資料行。  
  
 *cbUserData*[in]  
 使用者檔案中此欄位之資料的最大長度 (以位元組為單位)，不包括任何長度指標或結束字元的長度。  
  
 將 **cbUserData** 設定為 BCP_LENGTH_NULL 表示資料檔案欄位中的所有值都會 (或應該) 設定為 NULL。 將 **cbUserData** 設定為 BCP_LENGTH_VARIABLE 表示系統應該決定每個欄位的資料長度。 對於某些欄位而言，這可能表示長度/null 指標會在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複本之資料前產生，或者表示該指標應該會在複製到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的資料中出現。  
  
 對於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 字元和二進位資料類型而言，**cbUserData** 可以是 BCP_LENGTH_VARIABLE、BCP_LENGTH_NULL、0 或某個正數值。 如果 **cbUserData** 為 BCP_LENGTH_VARIABLE，系統會使用長度指標 (如果存在) 或結束字元順序來決定資料的長度。 如果同時提供長度指標與結束字元順序，大量複製會使用導致複製最少量資料者。 如果 **cbUserData** 為 BCP_LENGTH_VARIABLE、資料類型為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 字元或二進位類型，而且長度指標和結束字元順序都未指定，系統會傳回錯誤訊息。  
  
 如果 **cbUserData** 為 0 或正值，則系統會使用 **cbUserData** 當作最大的資料長度。 不過，如果除了正的 **cbUserData** 之外，也提供長度指標或結束字元順序，系統會使用導致複製最少量資料的方式決定資料長度。  
  
 **cbUserData** 值表示資料的位元組計數。 如果字元資料是以 Unicode 寬字元表示，則 **cbUserData** 正參數值表示字元數乘以每個字元的大小 (以位元組為單位)。  
  
 *pbUserDataTerm*[size_is][in]  
 用於此欄位的結束字元順序。 此參數主要用於字元資料類型，因為其他所有類型都屬固定長度；如果是二進位資料，則需要一個長度指標，才能正確記錄出現的位元組數目。  
  
 為避免結束已擷取的資料，或要指出使用者檔案中的資料未結束，將此參數設定為 NULL。  
  
 如果使用多種指定使用者檔案資料行長度的方式 (例如結束字元和長度指標，或結束字元和資料行長度最大值)，大量複製會選擇導致複製最少量資料的方式。  
  
 大量複製 API 會視需要執行 Unicode 到 MBCS 的字元轉換。 請務必確認結束字元位元組字串與位元組字串長度的設定正確。  
  
 *cbUserDataTerm*[in]  
 要用於此資料行的結束字元順序長度 (以位元組為單位)。 如果資料中沒有或不需要結束字元，將此值設定為 0。  
  
 *idxServerCol*[in]  
 此資料行在資料庫資料表中的序數位置。 第一個資料行編號為 1。 資料行的序數位置是由 **IColumnsInfo::GetColumnInfo** 或類似的方法所報告。 如果此值為 0，大量複製會在資料檔案中忽略此欄位。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 發生提供者特定的錯誤，如需詳細資訊，請使用 [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) 介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如，在呼叫這個方法之前，不會呼叫 [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) 方法。  
  
 E_INVALIDARG  
 此引數無效。  
  
 E_OUTOFMEMORY  
 記憶體不足的錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [執行大量複製作業](../../oledb/features/performing-bulk-copy-operations.md)  
  
  
