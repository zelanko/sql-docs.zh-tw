---
title: ErrorValueEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ErrorValueEnum
helpviewer_keywords:
- ErrorValueEnum enumeration [ADO]
ms.assetid: 9469ba3a-5e4f-4a10-bbb8-a51a6c9660ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18117be8dccc64f7ed2583170cf062145836f337
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932878"
---
# <a name="errorvalueenum"></a>ErrorValueEnum
指定 ADO 執行階段錯誤的類型。  
  
 列出錯誤號碼的三種形式：  
  
-   正十進位-十進位格式之完整數位的低兩個位元組。 這個數位會顯示在預設的 Visual Basic 錯誤訊息] 對話方塊中。 例如，執行階段錯誤 ' 3707 '。  
  
-   負十進位-完整錯誤號碼的十進位轉譯。  
  
-   十六進位-完整錯誤號碼的十六進位標記法。 Windows 設施程式碼位於第四個數字。 ADO 錯誤*號碼的設施*程式碼為。例如： 0x800***A***0E7B。  
  
> [!NOTE]
>  OLE DB 錯誤可能會傳遞至您的 ADO 應用程式。 一般而言，這些可以由 Windows 設備代碼*4*來識別。 例如，0x800***4***。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adErrBoundToCommand**|3707-2146824581 0x800A0E7B|無法變更具有**命令**物件作為其來源之**記錄集**物件的**ActiveConnection**屬性。|  
|**adErrCannotComplete**|3732-2146824556 0x800A0E94|伺服器無法完成操作。|  
|**adErrCantChangeConnection**|3748-2146824540 0x800A0EA4|連接被拒。 您所要求的新連接具有與已使用的不同的特性。|  
|**adErrCantChangeProvider**|3220-2146825068 0X800A0C94|提供的提供者與已在使用中的提供者不同。|  
|**adErrCantConvertvalue**|3724-2146824564 0x800A0E8C|因為符號不相符或資料溢位以外的原因，所以無法轉換資料值。 例如，轉換會有截斷的資料。|  
|**adErrCantCreate**|3725-2146824563 0x800A0E8D|因為欄位資料類型未知，或提供者的資源不足，無法執行作業，所以無法設定或抓取資料值。|  
|**adErrCatalogNotSet**|3747-2146824541 0x800A0EA3|作業需要有效的**ParentCatalog**。|  
|**adErrColumnNotOnThisRow**|3726-2146824562 0x800A0E8E|記錄不包含此欄位。|  
|**adErrDataConversion**|3421-2146824867 0x800A0D5D|應用程式會針對目前的作業使用錯誤類型的值。|  
|**adErrDataOverflow**|3721-2146824567 0x800A0E89|資料值太大，無法以欄位資料類型表示。|  
|**adErrDelResOutOfScope**|3738-2146824550 0x800A0E9A|要刪除之物件的 URL 超出目前記錄的範圍。|  
|**adErrDenyNotSupported**|3750-2146824538 0x800A0EA6|提供者不支援共用限制。|  
|**adErrDenyTypeNotSupported**|3751-2146824537 0x800A0EA7|提供者不支援要求的共用限制種類。|  
|**adErrFeatureNotAvailable**|3251-2146825037 0x800A0CB3|物件或提供者無法執行要求的作業。|  
|**adErrFieldsUpdateFailed**|3749-2146824539 0x800A0EA5|欄位更新失敗。 如需詳細資訊，請檢查個別欄位物件的**Status**屬性。|  
|**adErrIllegalOperation**|3219-2146825069 0x800A0C93|在此內容中不允許作業。|  
|**adErrIntegrityViolation**|3719-2146824569 0x800A0E87|資料值與欄位的完整性條件約束衝突。|  
|**adErrInTransaction**|3246-2146825042 0x800A0CAE|在交易中，無法明確關閉**連接**物件。|  
|**adErrInvalidArgument**|3001-2146825287 0x800A0BB9|引數的類型錯誤、超出可接受的範圍，或是彼此衝突。|  
|**adErrInvalidConnection**|3709-2146824579 0x800A0E7D|無法使用連接來執行此作業。 在此內容中，它已關閉或無效。|  
|**adErrInvalidParamInfo**|3708-2146824580 0x800A0E7C|**參數**物件的定義不正確。 提供不一致或不完整的資訊。|  
|**adErrInvalidTransaction**|3714-2146824574 0x800A0E82|協調交易無效或尚未啟動。|  
|**adErrInvalidURL**|3729-2146824559 0x800A0E91|URL 包含不正確字元。 請確定已正確輸入 URL。|  
|**adErrItemNotFound**|3265-2146825023 0x800A0CC1|在對應到所要求之名稱或序數的集合中找不到專案。|  
|**adErrNoCurrentRecord**|3021-2146825267 0x800A0BCD|[ **BOF** ] 或 [ **EOF** ] 為 True，或目前的記錄已刪除。 要求的作業需要目前的記錄。|  
|**adErrNotExecuting**|3715-2146824573 0x800A0E83|無法在執行作業時執行作業。|  
|**adErrNotReentrant**|3710-2146824578 0x800A0E7E|處理事件時無法執行作業。|  
|**adErrObjectClosed**|3704-2146824584 0x800A0E78|當物件關閉時，不允許操作。|  
|**adErrObjectInCollection**|3367-2146824921 0x800A0D27|物件已在集合中。 無法附加。|  
|**adErrObjectNotSet**|3420-2146824868 0x800A0D5C|物件不再有效。|  
|**adErrObjectOpen**|3705-2146824583 0x800A0E79|當物件開啟時，不允許執行作業。|  
|**adErrOpeningFile**|3002-2146825286 0x800A0BBA|無法開啟檔案。|  
|**adErrOperationCancelled**|3712-2146824576 0x800A0E80|使用者已取消操作。|  
|**adErrOutOfSpace**|3734-2146824554 0x800A0E96|無法執行作業。 提供者無法取得足夠的儲存空間。|  
|**adErrPermissionDenied**|3720-2146824568 0x800A0E88|許可權不足導致無法寫入欄位。|  
|**adErrProviderFailed**|3000-2146825288 0x800A0BB8|提供者未執行要求的作業。|  
|**adErrProviderNotFound**|3706-2146824582 0x800A0E7A|找不到提供者。 可能未正確安裝。|  
|**adErrReadFile**|3003-2146825285 0x800A0BBB|無法讀取檔案。|  
|**adErrResourceExists**|3731-2146824557 0x800A0E93|無法執行複製操作。 以目的地 URL 命名的物件已經存在。 指定**adCopyOverwrite**以取代物件。|  
|**adErrResourceLocked**|3730-2146824558 0x800A0E92|由指定 URL 所表示的物件已由一或多個其他進程鎖定。 請等候進程完成，然後再次嘗試操作。|  
|**adErrResourceOutOfScope**|3735-2146824553 0x800A0E97|來源或目的地 URL 超出目前記錄的範圍。|  
|**adErrSchemaViolation**|3722-2146824566 0x800A0E8A|資料值與欄位的資料類型或條件約束相衝突。|  
|**adErrSignMismatch**|3723-2146824565 0x800A0E8B|轉換失敗，因為資料值已簽署，而且提供者所使用的欄位資料類型不帶正負號。|  
|**adErrStillConnecting**|3713-2146824575 0x800A0E81|以非同步方式連接時，無法執行作業。|  
|**adErrStillExecuting**|3711-2146824577 0x800A0E7F|以非同步方式執行時，無法執行作業。|  
|**adErrTreePermissionDenied**|3728-2146824560 0x800A0E90|許可權不足以存取樹狀目錄或子樹。|  
|**adErrUnavailable**|3736-2146824552 0x800A0E98|作業未完成，且狀態為 [無法使用]。 欄位可能無法使用，或未嘗試操作。|  
|**adErrUnsafeOperation**|3716-2146824572 0x800A0E84|這部電腦上的安全性設定會防止存取另一個網域上的資料來源。|  
|**adErrURLDoesNotExist**|3727-2146824561 0x800A0E8F|來源 URL 或目的地 URL 的父系不存在。|  
|**adErrURLNamedRowDoesNotExist**|3737-2146824551 0x800A0E99|此 URL 所命名的記錄不存在。|  
|**adErrVolumeNotFound**|3733-2146824555 0x800A0E95|提供者找不到 URL 所指示的儲存裝置。 請確定已正確輸入 URL。|  
|**adErrWriteFile**|3004-2146825284 0x800A0BBC|寫入檔案失敗。|  
|**adWrnSecurityDialog**|3717-2146824571 0x800A0E85|僅供內部使用。 請勿使用。|  
|**adWrnSecurityDialogHeader**|3718-2146824570 0x800A0E86|僅供內部使用。 請勿使用。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
 只會定義下列 ADO/WFC 對應項的子集。  
  
|持續性|  
|--------------|  
|AdoEnums.ErrorValue.BOUNDTOCOMMAND|  
|AdoEnums.ErrorValue.DATACONVERSION|  
|AdoEnums.ErrorValue.FEATURENOTAVAILABLE|  
|AdoEnums.ErrorValue.ILLEGALOPERATION|  
|AdoEnums.ErrorValue.INTRANSACTION|  
|AdoEnums.ErrorValue.INVALIDARGUMENT|  
|AdoEnums.ErrorValue.INVALIDCONNECTION|  
|AdoEnums.ErrorValue.INVALIDPARAMINFO|  
|AdoEnums.ErrorValue.ITEMNOTFOUND|  
|AdoEnums.ErrorValue.NOCURRENTRECORD|  
|AdoEnums.ErrorValue.NOTEXECUTING|  
|AdoEnums.ErrorValue.NOTREENTRANT|  
|AdoEnums.ErrorValue.OBJECTCLOSED|  
|AdoEnums.ErrorValue.OBJECTINCOLLECTION|  
|AdoEnums.ErrorValue.OBJECTNOTSET|  
|AdoEnums.ErrorValue.OBJECTOPEN|  
|AdoEnums. ErrorValue. OPERATIONCANCELLED|  
|AdoEnums.ErrorValue.PROVIDERNOTFOUND|  
|AdoEnums.ErrorValue.STILLCONNECTING|  
|AdoEnums.ErrorValue.STILLEXECUTING|  
|AdoEnums.ErrorValue.UNSAFEOPERATION|  
  
## <a name="applies-to"></a>套用至  
 [Number 屬性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO 錯誤碼](../../../ado/guide/appendixes/ado-error-codes.md)
