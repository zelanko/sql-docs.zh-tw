---
title: ADO 錯誤參考 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], number reference
- errors [ADO], ErrorValueEnum
- ErrorValueEnum enumeration [ADO]
ms.assetid: f653393e-d4b0-4c34-ad5f-2bdf56bc1305
author: rothja
ms.author: jroth
ms.openlocfilehash: 774a1c17f579c9274b700e4e1fea682cc462ed29
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761384"
---
# <a name="ado-errors"></a>ADO 錯誤
**ErrorValueEnum**常數描述 ADO 錯誤值。 如需這些列舉常數的完整清單（包括值），請參閱[附錄 B： ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)。 本節將檢查一些較有趣的錯誤，並說明一些可能引發問題的特定情況，或是解決問題的解決方案。 **ErrorValueEnum**常數和簡短的正十進位數都會列出。

|數字|ErrorValueEnum 常數|描述/可能的原因|
|------------|-----------------------------|----------------------------------|
|**3000**|**adErrProviderFailed**|提供者無法執行要求的作業。|
|**3001**|**adErrInvalidArgument**|引數的類型錯誤、超出可接受的範圍，或是彼此衝突。 此錯誤通常是因為 SQL SELECT 語句中的印刷錯誤所造成。 例如，拼錯的功能變數名稱或資料表名稱可能會產生此錯誤。 當 SELECT 語句中名為的欄位或資料表不存在於資料存放區時，也可能會發生此錯誤。|
|**3002**|**adErrOpeningFile**|無法開啟檔案。 指定了拼錯的檔案名，或檔案已移動、重新命名或刪除。 透過網路，磁片磁碟機可能暫時無法使用，或者網路流量可能會阻止連線。|
|**3003**|**adErrReadFile**|無法讀取檔案。 檔案的名稱指定不正確、檔案可能已移動或刪除，或是檔案可能已損毀。|
|**3004**|**adErrWriteFile**|寫入檔案失敗。 您可能已關閉檔案，然後嘗試寫入檔案，或檔案可能已損毀。 如果檔案位於網路磁碟機機上，暫時性的網路狀況可能會阻止寫入網路磁碟機機。|
|**3021**|**adErrNoCurrentRecord**|[ **BOF** ] 或 [ **EOF** ] 為 True，或目前的記錄已刪除。 要求的作業需要目前的記錄。<br /><br /> 嘗試使用 [**尋找**] 或 [**搜尋**] 將記錄指標移至所需的記錄來更新記錄。 如果找不到記錄， **EOF**將會是 True。 當失敗的**AddNew**或**Delete**之後，此錯誤也會發生，因為這些方法失敗時沒有最新的記錄。|
|**3219**|**adErrIllegalOperation**|在此內容中不允許作業。|
|**3220**|**adErrCantChangeProvider**|提供的提供者與已在使用中的提供者不同。|
|**3246**|**adErrInTransaction**|在交易中，無法明確關閉**連接**物件。 無法關閉目前參與交易的**記錄集**或**連接**物件。 在關閉物件之前，請先呼叫**RollbackTrans**或**CommitTrans** 。|
|**3251**|**adErrFeatureNotAvailable**|物件或提供者無法執行要求的作業。 某些作業相依于特定的提供者版本。|
|**3265**|**adErrItemNotFound**|在對應到所要求之名稱或序數的集合中找不到專案。 指定了不正確的欄位或資料表名稱。|
|**3367**|**adErrObjectInCollection**|物件已在集合中。 無法附加。 無法將物件加入至相同的集合兩次。|
|**3420**|**adErrObjectNotSet**|物件不再有效。|
|**3421**|**adErrDataConversion**|應用程式會針對目前的作業使用錯誤類型的值。 例如，您可能已提供字串給預期資料流程的作業。|
|**3704**|**adErrObjectClosed**|當物件關閉時，不允許操作。 **連接**或**記錄集**已關閉。 例如，某些其他常式可能已關閉全域物件。 您可以在嘗試作業之前，先檢查**State**屬性來避免這個錯誤。|
|**3705**|**adErrObjectOpen**|當物件開啟時，不允許執行作業。 無法開啟開啟的物件。 欄位不能附加至開啟的**記錄集**。|
|**3706**|**adErrProviderNotFound**|找不到提供者。 可能未正確安裝。<br /><br /> 提供者的名稱可能不正確，指定的提供者可能未安裝在執行程式碼的電腦上，或是安裝可能已損毀。|
|**3707**|**adErrBoundToCommand**|無法變更**記錄集**物件的**ActiveConnection**屬性，其具有做為其來源的**命令**物件。 應用程式嘗試將新的**連接**物件指派給具有**命令**物件作為其來源的**記錄集**。|
|**3708**|**adErrInvalidParamInfo**|**參數**物件定義不正確。 提供不一致或不完整的資訊。|
|**3709**|**adErrInvalidConnection**|無法使用連接來執行此作業。 在此內容中，它已關閉或無效。|
|**3710**|**adErrNotReentrant**|處理事件時無法執行作業。 無法在導致事件再次引發的事件處理常式內執行作業。 例如，不應從**WillMove**事件處理常式內呼叫導覽方法。|
|**3711**|**adErrStillExecuting**|以非同步方式執行時，無法執行作業。|
|**3712**|**adErrOperationCancelled**|使用者已取消操作。 應用程式已呼叫**CancelUpdate**或**CancelBatch**方法，且目前的作業已取消。|
|**3713**|**adErrStillConnecting**|以非同步方式連接時，無法執行作業。|
|**3714**|**adErrInvalidTransaction**|協調交易無效或尚未啟動。|
|**3715**|**adErrNotExecuting**|無法在執行作業時執行作業。|
|**3716**|**adErrUnsafeOperation**|此電腦上的安全設定禁止存取另一個網域上的資料來源。|
|**3717**|**adWrnSecurityDialog**|僅供內部使用。 請勿使用。 （為了完整性起見，已包含專案。 此錯誤不應出現在您的程式碼中。）|
|**3718**|**adWrnSecurityDialogHeader**|僅供內部使用。 請勿使用。 （為了完整性而包含的專案。 此錯誤不應出現在您的程式碼中。）|
|**3719**|**adErrIntegrityViolation**|資料值與欄位的完整性條件約束衝突。 **欄位**的新值會導致重複的索引鍵。 形成兩個記錄之間關聯性之一端的值可能不是可更新的。|
|**3720**|**adErrPermissionDenied**|許可權不足導致無法寫入欄位。 連接字串中所指定的使用者沒有適當的許可權可寫入**欄位**。|
|**3721**|**adErrDataOverflow**|資料值太大，無法以欄位資料類型表示。 指派給預定欄位的數值太大。 例如，將長整數值指派給短整數位段。|
|**3722**|**adErrSchemaViolation**|資料值與欄位的資料類型或條件約束相衝突。 資料存放區具有與**域**值不同的驗證條件約束。|
|**3723**|**adErrSignMismatch**|轉換失敗，因為資料值已簽署，而且提供者所使用的欄位資料類型不帶正負號。|
|**3724**|**adErrCantConvertvalue**|因為符號不相符或資料溢位以外的原因，所以無法轉換資料值。 例如，轉換會有截斷的資料。|
|**3725**|**adErrCantCreate**|因為欄位資料類型未知，或提供者的資源不足，無法執行作業，所以無法設定或抓取資料值。|
|**3726**|**adErrColumnNotOnThisRow**|記錄不包含此欄位。 指定了不正確的功能變數名稱，或參考了目前記錄之**Fields**集合中的欄位。|
|**3727**|**adErrURLDoesNotExist**|來源 URL 或目的地 URL 的父系不存在。 來源或目的地 URL 中有打字錯誤。 您可能會想要 `https://mysite/photo/myphoto.jpg` 改為實際擁有 `https://mysite/photos/myphoto.jpg` 。 父 URL 中的印刷錯誤（在此案例中為*相片*而不是*相片*）導致錯誤。|
|**3728**|**adErrTreePermissionDenied**|許可權不足以存取樹狀目錄或子樹。 連接字串中所指定的使用者沒有適當的許可權。|
|**3729**|**adErrInvalidURL**|URL 包含不正確字元。 請確定已正確輸入 URL。 URL 會遵循向目前提供者註冊的配置（例如，針對 HTTP 註冊網際網路發行提供者）。|
|**3730**|**adErrResourceLocked**|由指定 URL 所表示的物件已由一或多個其他進程鎖定。 請等候進程完成，然後再次嘗試操作。 您嘗試存取的物件已由另一位使用者或您應用程式中的另一個進程鎖定。 這最有可能發生在多使用者的環境中。|
|**3731**|**adErrResourceExists**|無法執行複製操作。 以目的地 URL 命名的物件已經存在。 指定**adCopyOverwrite**以取代物件。 如果您在複製目錄中的檔案時未指定**adCopyOverwrite** ，當您嘗試複製的專案已存在於目的地位置時，複製就會失敗。|
|**3732**|**adErrCannotComplete**|伺服器無法完成操作。 這可能是因為伺服器與其他作業忙碌，或資源不足所導致。|
|**3733**|**adErrVolumeNotFound**|提供者找不到 URL 所指示的儲存裝置。 請確定已正確輸入 URL。 儲存裝置的 URL 可能不正確，但可能是因為其他原因而發生此錯誤。 裝置可能已離線，或大量的網路流量可能會導致無法進行連線。|
|**3734**|**adErrOutOfSpace**|無法執行作業。 提供者無法取得足夠的儲存空間。 伺服器上的暫存檔案可能沒有足夠的 RAM 或硬碟空間。|
|**3735**|**adErrResourceOutOfScope**|來源或目的地 URL 超出目前記錄的範圍。|
|**3736**|**adErrUnavailable**|作業無法完成，且狀態為 [無法使用]。 欄位可能無法使用，或未嘗試操作。 另一位使用者可能已變更或刪除您嘗試存取的欄位。|
|**3737**|**adErrURLNamedRowDoesNotExist**|此 URL 所命名的記錄不存在。 嘗試使用**記錄**物件開啟檔案時，檔案名或檔案的路徑拼錯。|
|**3738**|**adErrDelResOutOfScope**|要刪除之物件的 URL 超出目前記錄的範圍。|
|**3747**|**adErrCatalogNotSet**|作業需要有效的**ParentCatalog**。|
|**3748**|**adErrCantChangeConnection**|連接被拒。 您所要求的新連接具有與已使用的不同的特性。|
|**3749**|**adErrFieldsUpdateFailed**|欄位更新失敗。 如需進一步資訊，請檢查個別欄位物件的**Status**屬性。 在兩種情況下，可能會發生此錯誤：變更**欄位**物件在變更或將記錄新增至資料庫的過程中的值;以及變更**Field**物件本身的屬性時。<br /><br /> **記錄**或**記錄集**更新失敗，因為目前記錄中的其中一個欄位發生問題。 列舉**Fields**集合，並檢查每個欄位的**Status**屬性，以判斷問題的原因。|
|**3750**|**adErrDenyNotSupported**|提供者不支援共用限制。 嘗試限制檔案共用，且您的提供者不支援此概念。|
|**3751**|**adErrDenyTypeNotSupported**|提供者不支援要求的共用限制種類。 嘗試建立您的提供者不支援的特定類型檔案共用限制。 請參閱提供者的檔，以判斷支援哪些檔案共用限制。|
