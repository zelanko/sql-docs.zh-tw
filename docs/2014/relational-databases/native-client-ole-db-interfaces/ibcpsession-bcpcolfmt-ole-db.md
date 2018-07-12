---
title: 'Ibcpsession:: Bcpcolfmt (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IBCPSession::BCPColFmt (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPColFmt method
ms.assetid: 2852f4ba-f1c6-4c4c-86b2-b77e4abe70de
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea0872d071893e7d88a5d52d677702a984e49f02
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426717"
---
# <a name="ibcpsessionbcpcolfmt-ole-db"></a>IBCPSession::BCPColFmt (OLE DB)
  在程式變數與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料行之間建立繫結。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT BCPColFmt(   
DBORDINALidxUserDataCol,  
inteUserDataType,  
intcbIndicator,  
intcbUserData,  
BYTE *pbUserDataTerm,  
intcbUserDataTerm,  
DBORDINALidxServerCol);  
```  
  
## <a name="remarks"></a>備註  
 **BCPColFmt**方法用來建立 BCP 資料檔欄位之間的繫結和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料行。 它會使用資料行的長度、類型、結束字元和前置長度當做參數，並為個別欄位設定每一個屬性。  
  
 如果使用者選擇互動模式，就會呼叫這個方法兩次；一次是根據預設值設定資料行格式 (預設值是根據伺服器資料行的類型)，另一次是根據互動模式期間選擇之用戶端的資料行類型，針對每一個資料行設定格式。  
  
 在非互動模式中，每一個資料行只會呼叫這個方法一次，以便將每一個資料行的類型設定為字元或原生類型，或是設定資料行和資料列結束字元。  
  
 **BCPColFmt**方法可讓您指定大量複製的使用者檔案格式。 針對大量複製，格式包含下列部分：  
  
-   從使用者檔案欄位對應至資料庫資料行。  
  
-   每個使用者檔案欄位的資料類型。  
  
-   每個欄位的選擇性指標長度。  
  
-   每個使用者檔案欄位的資料最大長度。  
  
-   每個欄位的選擇性結束位元組順序。  
  
-   選擇性結束位元組順序的長度。  
  
 每次呼叫**BCPColFmt**指定一個使用者檔案欄位的格式。 例如，若要變更在五個欄位的使用者資料檔案的三個欄位的預設設定，請先呼叫`BCPColumns(5)`，然後呼叫**BCPColFmt**五次，其中三次呼叫會設定您的自訂格式。 針對其餘的兩個呼叫中，設定*eUserDataType*為 BCP_TYPE_DEFAULT，並將*cbIndicator*， *cbUserData*，和*cbUserDataTerm*至 0、bcp_variable_length 和 0 分別。 此程序會複製全部五個資料行，其中三個為您自訂的格式，而另兩個為預設格式。  
  
> [!NOTE]  
>  [Ibcpsession:: Bcpcolumns](ibcpsession-bcpcolumns-ole-db.md)任何呼叫之前，必須呼叫方法**BCPColFmt**。 您必須呼叫**BCPColFmt**使用者檔案中的每個資料行一次。 呼叫**BCPColFmt**一次以上的任何使用者檔案資料行導致錯誤。  
  
 您不必將使用者檔案中的所有資料複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 若要略過資料行，請指定資料行的資料格式，並將 idxServerCol 參數設定為 0。 為了略過欄位，您仍然需要所有資訊，才能讓此方法正確運作。  
  
 **附註** [ibcpsession:: Bcpwritefmt](ibcpsession-bcpwritefmt-ole-db.md)函式可以用來保存透過所提供的格式規格**BCPColFmt**。  
  
## <a name="arguments"></a>引數  
 *idxUserDataCol*[in]  
 使用者的資料檔案中的欄位索引。  
  
 *eUserDataType*[in]  
 使用者的資料檔案中欄位的資料類型。 可用的資料類型會列在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 標頭檔 (sqlncli.h)，為 BCP_TYPE_XXX 格式，例如 BCP_TYPE_SQLINT4。 如果指定了 BCP_TYPE_DEFAULT 值，提供者會嘗試使用與資料表或檢視表資料行類型相同的類型。 大量複製作業，共[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到檔案時`eUserDataType`引數為 BCP_TYPE_SQLDECIMAL 或 BCP_TYPE_SQLNUMERIC:  
  
-   如果來源資料行不是小數或數值，便會使用預設的有效位數和小數位數。  
  
-   如果來源資料行是小數或數值，則會使用來源資料行的有效位數和小數位數。  
  
 *cbIndicator*[in]  
 欄位的前置長度。 預設值為 BCP_PREFIX_DEFAULT。 此前置詞的有效長度為 0、1、2、4 和 8。 前置詞大小 8 最常用來指示此欄位已分成若干區塊。 這可用來有效率地大量複製大型值類型的資料行。  
  
 *cbUserData*[in]  
 使用者檔案中此欄位之資料的最大長度 (以位元組為單位)，不包括任何長度指標或結束字元的長度。  
  
 設定`cbUserData`為 BCP_LENGTH_NULL 表示檔案欄位的資料中的所有值，或應該設為 NULL。 設定`cbUserData`為 BCP_LENGTH_VARIABLE 表示系統應該決定每個欄位的資料長度。 對於某些欄位而言，這可能表示長度/null 指標會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複本之資料前產生，或者表示該指標應該會在複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料中出現。  
  
 針對[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字元和二進位資料類型，`cbUserData`可以是 BCP_LENGTH_VARIABLE、 BCP_LENGTH_NULL、 0 或某些正值。 如果`cbUserData`為 BCP_LENGTH_VARIABLE，系統會使用長度指標，如果存在或結束字元順序來決定資料的長度。 如果同時提供長度指標與結束字元順序，大量複製會使用導致複製最少量資料者。 如果`cbUserData`為 BCP_LENGTH_VARIABLE、 資料型別是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字元或二進位類型，而且長度指標和結束字元順序都不指定，系統會傳回錯誤訊息。  
  
 如果`cbUserData`為 0 或正值，則系統會使用`cbUserData`為最大資料長度。 不過，如果除了正`cbUserData`提供長度指標或結束字元順序，系統會使用產生最少量複製資料的方法來決定資料長度。  
  
 `cbUserData`值表示資料的位元組計數。 如果字元資料以 Unicode 寬字元，則正`cbUserData`參數值表示乘以的大小，以位元組為單位，每個字元的字元數。  
  
 *pbUserDataTerm*[size_is][in]  
 用於此欄位的結束字元順序。 此參數主要用於字元資料類型，因為其他所有類型都屬固定長度；如果是二進位資料，則需要一個長度指標，才能正確記錄出現的位元組數目。  
  
 為避免結束已擷取的資料，或要指出使用者檔案中的資料未結束，將此參數設定為 NULL。  
  
 如果使用多種指定使用者檔案資料行長度的方式 (例如結束字元和長度指標，或結束字元和資料行長度最大值)，大量複製會選擇導致複製最少量資料的方式。  
  
 大量複製 API 會視需要執行 Unicode 到 MBCS 的字元轉換。 請務必確認結束字元位元組字串與位元組字串長度的設定正確。  
  
 *cbUserDataTerm*[in]  
 要用於此資料行的結束字元順序長度 (以位元組為單位)。 如果資料中沒有或不需要結束字元，將此值設定為 0。  
  
 *idxServerCol*[in]  
 此資料行在資料庫資料表中的序數位置。 第一個資料行編號為 1。 資料行的序數位置由報告**icolumnsinfo:: Getcolumninfo**或類似的方法。 如果此值為 0，大量複製會在資料檔案中忽略此欄位。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_FAIL  
 發生提供者特有的錯誤，如需詳細的資訊，請使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如， [ibcpsession:: Bcpinit](ibcpsession-bcpinit-ole-db.md)方法不會呼叫這個方法之前呼叫。  
  
 E_INVALIDARG  
 此引數無效。  
  
 E_OUTOFMEMORY  
 記憶體不足的錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [執行大量複製作業](../native-client/features/performing-bulk-copy-operations.md)  
  
  
