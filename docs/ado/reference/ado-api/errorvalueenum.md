---
description: ErrorValueEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f3dfcb5e806ad67a17a5899a4b930eedab0928f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443930"
---
# <a name="errorvalueenum"></a>ErrorValueEnum
指定 ADO 執行階段錯誤的類型。  
  
 列出三種形式的錯誤號碼：  
  
-   正整數-十進位格式之完整數位的最小2個位元組。 這個數位會顯示在預設 Visual Basic 錯誤訊息] 對話方塊中。 例如，執行階段錯誤 ' 3707 '。  
  
-   負十進位-完整錯誤號碼的十進位轉譯。  
  
-   十六進位-完整錯誤號碼的十六進位標記法。 Windows 設備碼為第四個數字。 ADO 錯誤 *號碼的設備碼是。* 例如 ***： 0x800 0E7B***。  
  
> [!NOTE]
>  OLE DB 錯誤可能會傳遞至您的 ADO 應用程式。 一般而言，這些可由 Windows 的 *4 個*設備碼來識別。 例如，0x800***4***。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adErrBoundToCommand**|3707-2146824581 0x800A0E7B|無法變更記錄集物件的 **ActiveConnection** 屬性，該 **記錄集** 物件的 **命令** 物件為其來源。|  
|**adErrCannotComplete**|3732-2146824556 0x800A0E94|伺服器無法完成操作。|  
|**adErrCantChangeConnection**|3748-2146824540 0x800A0EA4|連接遭到拒絕。 您所要求的新連線具有不同的特性，但其特性不同于已使用的連接。|  
|**adErrCantChangeProvider**|3220-2146825068 0X800A0C94|提供的提供者與已使用的提供者不同。|  
|**adErrCantConvertvalue**|3724-2146824564 0x800A0E8C|由於符號不符或資料溢位以外的原因而無法轉換資料值。 例如，轉換會有截斷的資料。|  
|**adErrCantCreate**|3725-2146824563 0x800A0E8D|無法設定或抓取資料值，因為欄位資料類型未知，或提供者沒有足夠的資源可執行作業。|  
|**adErrCatalogNotSet**|3747-2146824541 0x800A0EA3|作業需要有效的 **ParentCatalog**。|  
|**adErrColumnNotOnThisRow**|3726-2146824562 0x800A0E8E|記錄不包含此欄位。|  
|**adErrDataConversion**|3421-2146824867 0x800A0D5D|應用程式會針對目前的作業使用錯誤類型的值。|  
|**adErrDataOverflow**|3721-2146824567 0x800A0E89|資料值太大，無法以欄位資料類型表示。|  
|**adErrDelResOutOfScope**|3738-2146824550 0x800A0E9A|要刪除之物件的 URL 超出目前記錄的範圍。|  
|**adErrDenyNotSupported**|3750-2146824538 0x800A0EA6|提供者不支援共用限制。|  
|**adErrDenyTypeNotSupported**|3751-2146824537 0x800A0EA7|提供者不支援所要求的共用限制類型。|  
|**adErrFeatureNotAvailable**|3251-2146825037 0x800A0CB3|物件或提供者無法執行要求的操作。|  
|**adErrFieldsUpdateFailed**|3749-2146824539 0x800A0EA5|欄位更新失敗。 如需詳細資訊，請檢查個別欄位物件的 **Status** 屬性。|  
|**adErrIllegalOperation**|3219-2146825069 0x800A0C93|此內容中不允許作業。|  
|**adErrIntegrityViolation**|3719-2146824569 0x800A0E87|資料值與欄位的完整性條件約束衝突。|  
|**adErrInTransaction**|3246-2146825042 0x800A0CAE|在交易中，無法明確關閉**連接**物件。|  
|**adErrInvalidArgument**|3001-2146825287 0x800A0BB9|引數的類型不正確、不在可接受的範圍內，或彼此衝突。|  
|**adErrInvalidConnection**|3709-2146824579 0x800A0E7D|無法使用連接來執行此作業。 在此內容中，它可能已關閉或無效。|  
|**adErrInvalidParamInfo**|3708-2146824580 0x800A0E7C|**參數** 物件的定義不正確。 提供不一致或不完整的資訊。|  
|**adErrInvalidTransaction**|3714-2146824574 0x800A0E82|協調交易無效或尚未啟動。|  
|**adErrInvalidURL**|3729-2146824559 0x800A0E91|URL 包含不正確字元。 請確定 URL 的類型正確無誤。|  
|**adErrItemNotFound**|3265-2146825023 0x800A0CC1|在對應至所要求名稱或序數的集合中找不到專案。|  
|**adErrNoCurrentRecord**|3021-2146825267 0x800A0BCD|**BOF**或**EOF**為 True，或目前的記錄已刪除。 要求的作業需要目前的記錄。|  
|**adErrNotExecuting**|3715-2146824573 0x800A0E83|無法執行作業，但無法執行。|  
|**adErrNotReentrant**|3710-2146824578 0x800A0E7E|處理事件時，無法執行操作。|  
|**adErrObjectClosed**|3704-2146824584 0x800A0E78|當物件關閉時，不允許作業。|  
|**adErrObjectInCollection**|3367-2146824921 0x800A0D27|物件已經在集合中。 無法附加。|  
|**adErrObjectNotSet**|3420-2146824868 0x800A0D5C|物件不再有效。|  
|**adErrObjectOpen**|3705-2146824583 0x800A0E79|當物件開啟時，不允許作業。|  
|**adErrOpeningFile**|3002-2146825286 0x800A0BBA|無法開啟檔案。|  
|**adErrOperationCancelled**|3712-2146824576 0x800A0E80|使用者已取消作業。|  
|**adErrOutOfSpace**|3734-2146824554 0x800A0E96|無法執行操作。 提供者無法取得足夠的儲存空間。|  
|**adErrPermissionDenied**|3720-2146824568 0x800A0E88|許可權不足會防止寫入欄位。|  
|**adErrProviderFailed**|3000-2146825288 0x800A0BB8|提供者未執行要求的操作。|  
|**adErrProviderNotFound**|3706-2146824582 0x800A0E7A|找不到提供者。 可能未正確安裝。|  
|**adErrReadFile**|3003-2146825285 0x800A0BBB|無法讀取檔案。|  
|**adErrResourceExists**|3731-2146824557 0x800A0E93|無法執行複製作業。 目的地 URL 所命名的物件已經存在。 指定 **adCopyOverwrite** 來取代物件。|  
|**adErrResourceLocked**|3730-2146824558 0x800A0E92|由指定的 URL 表示的物件已被一或多個其他進程鎖定。 請等候進程完成，然後再次嘗試操作。|  
|**adErrResourceOutOfScope**|3735-2146824553 0x800A0E97|來源或目的地 URL 超出目前記錄的範圍。|  
|**adErrSchemaViolation**|3722-2146824566 0x800A0E8A|資料值與欄位的資料類型或條件約束衝突。|  
|**adErrSignMismatch**|3723-2146824565 0x800A0E8B|轉換失敗，因為資料值已簽署，而提供者使用的欄位資料類型未簽署。|  
|**adErrStillConnecting**|3713-2146824575 0x800A0E81|非同步連接時無法執行操作。|  
|**adErrStillExecuting**|3711-2146824577 0x800A0E7F|以非同步方式執行時，無法執行操作。|  
|**adErrTreePermissionDenied**|3728-2146824560 0x800A0E90|許可權不足以存取樹狀結構或子樹。|  
|**adErrUnavailable**|3736-2146824552 0x800A0E98|作業未完成，且狀態為無法使用。 欄位可能無法使用，或未嘗試操作。|  
|**adErrUnsafeOperation**|3716-2146824572 0x800A0E84|此電腦上的安全設定會防止存取另一個網域上的資料來源。|  
|**adErrURLDoesNotExist**|3727-2146824561 0x800A0E8F|來源 URL 或目的地 URL 的父系不存在。|  
|**adErrURLNamedRowDoesNotExist**|3737-2146824551 0x800A0E99|這個 URL 所命名的記錄不存在。|  
|**adErrVolumeNotFound**|3733-2146824555 0x800A0E95|提供者找不到 URL 所指出的儲存裝置。 請確定 URL 的類型正確無誤。|  
|**adErrWriteFile**|3004-2146825284 0x800A0BBC|寫入檔案失敗。|  
|**adWrnSecurityDialog**|3717-2146824571 0x800A0E85|僅供內部使用。 請勿使用。|  
|**adWrnSecurityDialogHeader**|3718-2146824570 0x800A0E86|僅供內部使用。 請勿使用。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
 只會定義下列 ADO/WFC 對等專案的子集。  
  
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
|AdoEnums. ErrorValue. OPERATIONCANCELLED|  
|AdoEnums.ErrorValue.PROVIDERNOTFOUND|  
|AdoEnums.ErrorValue.STILLCONNECTING|  
|AdoEnums.ErrorValue.STILLEXECUTING|  
|AdoEnums.ErrorValue.UNSAFEOPERATION|  
  
## <a name="applies-to"></a>套用至  
 [Number 屬性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO 錯誤碼](../../../ado/guide/appendixes/ado-error-codes.md)
