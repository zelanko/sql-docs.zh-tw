---
title: ErrorValueEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ErrorValueEnum
helpviewer_keywords:
- ErrorValueEnum enumeration [ADO]
ms.assetid: 9469ba3a-5e4f-4a10-bbb8-a51a6c9660ea
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e040c1738513fcf96d84144090c531a4d14704e2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="errorvalueenum"></a>ErrorValueEnum
指定 ADO 執行階段錯誤的類型。  
  
 列出的錯誤號碼的三種形式：  
  
-   正數小 — 完整的十進位數字的低的兩個位元組。 這個數字會顯示在預設 Visual Basic 錯誤訊息對話方塊。 例如，執行階段錯誤 '3707'。  
  
-   負數的小數點，完整的錯誤數字的十進位的轉譯。  
  
-   十六進位 — 完整的錯誤號碼的十六進位表示法。 Windows 設備碼是在第四個的數字。 設備碼 ADO 錯誤號碼是*A*。例如： 0x800***A***0E7B。  
  
> [!NOTE]
>  OLE DB 錯誤可傳遞至 ADO 應用程式。 一般來說，識別這些程式的 Windows 設備碼*4*。 例如，0x800***4***。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adErrBoundToCommand**|3707-2146824581 0x800A0E7B|無法變更**ActiveConnection**屬性**資料錄集**具有物件**命令**作為其來源的物件。|  
|**adErrCannotComplete**|3732 -2146824556 0x800A0E94|伺服器無法完成作業。|  
|**adErrCantChangeConnection**|3748-2146824540 0x800A0EA4|已拒絕連線。 您要求新的連接都有不同於已使用的特性。|  
|**adErrCantChangeProvider**|3220 -2146825068 0X800A0C94|提供的提供者不同於已使用的一個。|  
|**adErrCantConvertvalue**|3724 -2146824564 0x800A0E8C|由於符號不符或資料溢位以外的原因而無法轉換資料值。 例如，轉換會有截斷資料。|  
|**adErrCantCreate**|3725-2146824563 0x800A0E8D|無法設定或擷取欄位資料型別為未知，或提供者有資源不足，無法執行作業，因為資料值。|  
|**adErrCatalogNotSet**|3747 -2146824541 0x800A0EA3|作業需要有效**ParentCatalog**。|  
|**adErrColumnNotOnThisRow**|3726-2146824562 0x800A0E8E|記錄不包含此欄位。|  
|**adErrDataConversion**|3421 -2146824867 0x800A0D5D|應用程式會使用目前的作業錯誤類型的值。|  
|**adErrDataOverflow**|3721 -2146824567 0x800A0E89|資料值太大而無法表示欄位資料型別。|  
|**adErrDelResOutOfScope**|3738 -2146824550 0x800A0E9A|要刪除物件的 URL 是記錄的在目前範圍之外。|  
|**adErrDenyNotSupported**|3750-2146824538 0x800A0EA6|提供者不支援共用限制。|  
|**adErrDenyTypeNotSupported**|3751-2146824537 0x800A0EA7|提供者不支援共用限制的要求的的類型。|  
|**adErrFeatureNotAvailable**|3251 -2146825037 0x800A0CB3|物件或提供者不能執行要求的作業。|  
|**adErrFieldsUpdateFailed**|3749-2146824539 0x800A0EA5|欄位更新失敗。 如需詳細資訊，請檢查**狀態**個別欄位物件的屬性。|  
|**adErrIllegalOperation**|3219 -2146825069 0x800A0C93|在此內容中不允許作業。|  
|**adErrIntegrityViolation**|3719 -2146824569 0x800A0E87|資料值欄位的完整性條件約束衝突。|  
|**adErrInTransaction**|3246 -2146825042 0x800A0CAE|**連接**物件無法在交易中明確地關閉。|  
|**adErrInvalidArgument**|3001 -2146825287 0x800A0BB9|引數的類型錯誤，超出可接受的範圍，或互相。|  
|**adErrInvalidConnection**|3709 -2146824579 0x800A0E7D|連接無法用來執行這項作業。 它是已關閉，或在此內容中無效。|  
|**adErrInvalidParamInfo**|3708 -2146824580 0x800A0E7C|**參數**物件的定義不正確。 提供不一致或不完整的資訊。|  
|**adErrInvalidTransaction**|3714 -2146824574 0x800A0E82|協調交易無效或尚未啟動。|  
|**adErrInvalidURL**|3729 -2146824559 0x800A0E91|URL 包含無效的字元。 請確定輸入的 URL 正確。|  
|**adErrItemNotFound**|3265 -2146825023 0x800A0CC1|對應到要求的名稱或序數集合中找不到項目。|  
|**adErrNoCurrentRecord**|3021 -2146825267 0x800A0BCD|任一**BOF**或**EOF**為 True，或目前的記錄已被刪除。 要求的作業需要目前的記錄。|  
|**adErrNotExecuting**|3715 -2146824573 0x800A0E83|未執行時，無法執行作業。|  
|**adErrNotReentrant**|3710-2146824578 0x800A0E7E|正在處理事件時，無法執行作業。|  
|**adErrObjectClosed**|3704 -2146824584 0x800A0E78|當物件已關閉時，不允許作業。|  
|**adErrObjectInCollection**|3367 -2146824921 0x800A0D27|物件已經在集合中。 無法附加。|  
|**adErrObjectNotSet**|3420-2146824868 0x800A0D5C|物件不再有效。|  
|**adErrObjectOpen**|容量 3705-2146824583 0x800A0E79|物件開啟時，不允許作業。|  
|**adErrOpeningFile**|3002-2146825286 0x800A0BBA|無法開啟檔案。|  
|**adErrOperationCancelled**|3712 -2146824576 0x800A0E80|使用者已取消作業。|  
|**adErrOutOfSpace**|3734 -2146824554 0x800A0E96|無法執行作業。 提供者無法取得足夠的儲存空間。|  
|**adErrPermissionDenied**|3720 -2146824568 0x800A0E88|沒有足夠的權限可防止寫入的欄位。|  
|**adErrProviderFailed**|3000 -2146825288 0x800A0BB8|提供者無法執行要求的作業。|  
|**adErrProviderNotFound**|3706-2146824582 0x800A0E7A|找不到提供者。 它可能未正確安裝。|  
|**adErrReadFile**|3003 -2146825285 0x800A0BBB|無法讀取檔案。|  
|**adErrResourceExists**|3731 -2146824557 0x800A0E93|無法執行複製作業。 物件名稱的目的地 URL 已經存在。 指定**adCopyOverwrite**取代物件。|  
|**adErrResourceLocked**|3730 -2146824558 0x800A0E92|指定的 URL 所代表的物件已鎖定一或多個其他處理程序。 請等待程序完成，然後再次嘗試操作。|  
|**adErrResourceOutOfScope**|3735-2146824553 0x800A0E97|來源或目的地 URL 是記錄的在目前範圍之外。|  
|**adErrSchemaViolation**|3722-2146824566 0x800A0E8A|資料值和資料類型或欄位的條件約束衝突。|  
|**adErrSignMismatch**|3723-2146824565 0x800A0E8B|轉換失敗，因為資料值為 signed，而提供者所使用的欄位資料類型不帶正負號。|  
|**adErrStillConnecting**|3713 -2146824575 0x800A0E81|以非同步方式連線時，無法執行作業。|  
|**adErrStillExecuting**|3711 -2146824577 0x800A0E7F|以非同步方式執行時，無法執行作業。|  
|**adErrTreePermissionDenied**|3728 -2146824560 0x800A0E90|權限還不足以存取樹狀目錄或樹狀子目錄。|  
|**adErrUnavailable**|3736 -2146824552 0x800A0E98|作業未完成，而無法使用狀態。 此欄位可能無法使用或不嘗試進行作業。|  
|**adErrUnsafeOperation**|3716-2146824572 0x800A0E84|在此電腦上的安全性設定會防止存取另一個網域的資料來源。|  
|**adErrURLDoesNotExist**|3727 -2146824561 0x800A0E8F|來源 URL 或目的地 URL 不存在的父系。|  
|**adErrURLNamedRowDoesNotExist**|3737 -2146824551 0x800A0E99|此 URL 命名的記錄不存在。|  
|**adErrVolumeNotFound**|3733 -2146824555 0x800A0E95|提供者找不到安全的 URL 的存放裝置。 請確定輸入的 URL 正確。|  
|**adErrWriteFile**|3004 -2146825284 0x800A0BBC|寫入檔案失敗。|  
|**adWrnSecurityDialog**|3717 -2146824571 0x800A0E85|僅供內部使用。 請勿使用。|  
|**adWrnSecurityDialogHeader**|3718 -2146824570 0x800A0E86|僅供內部使用。 請勿使用。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
 ADO/WFC 對等項目中的下列子集合所定義。  
  
|常數|  
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
|AdoEnums.ErrorValue.OPERATIONCANCELLED|  
|AdoEnums.ErrorValue.PROVIDERNOTFOUND|  
|AdoEnums.ErrorValue.STILLCONNECTING|  
|AdoEnums.ErrorValue.STILLEXECUTING|  
|AdoEnums.ErrorValue.UNSAFEOPERATION|  
  
## <a name="applies-to"></a>適用於  
 [Number 屬性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO 錯誤碼](../../../ado/guide/appendixes/ado-error-codes.md)
