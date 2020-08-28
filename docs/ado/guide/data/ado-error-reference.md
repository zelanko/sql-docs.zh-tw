---
description: ADO 錯誤參考
title: ADO 錯誤參考 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 83f3d5e9408180c4ff513f1457a2972a676fa726
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991739"
---
# <a name="ado-errors"></a>ADO 錯誤
**ErrorValueEnum**常數描述 ADO 誤差值。 如需這些列舉常數的完整清單（包括值），請參閱 [附錄 B： ADO 錯誤](../appendixes/appendix-b-ado-errors.md)。 本節將探討一些更有趣的錯誤，並說明可能引發這些錯誤的某些特定情況，或是解決問題的解決方案。 系統會列出 **ErrorValueEnum** 常數和簡短的正向十進位數。

|Number|ErrorValueEnum 常數|描述/可能的原因|
|------------|-----------------------------|----------------------------------|
|**3000**|**adErrProviderFailed**|提供者無法執行要求的操作。|
|**3001**|**adErrInvalidArgument**|引數的類型不正確、不在可接受的範圍內，或彼此衝突。 此錯誤通常是因為 SQL SELECT 語句中的印刷錯誤所造成。 例如，拼錯的功能變數名稱或資料表名稱可能會產生此錯誤。 當 SELECT 語句中指定的欄位或資料表不存在於資料存放區中時，也會發生此錯誤。|
|**3002**|**adErrOpeningFile**|無法開啟檔案。 指定了拼錯的檔案名，或檔案已移動、重新命名或刪除。 透過網路，磁片磁碟機可能暫時無法使用，或網路流量可能會導致連線中斷。|
|**3003**|**adErrReadFile**|無法讀取檔案。 檔案的名稱指定錯誤、檔案可能已被移動或刪除，或檔案可能已損毀。|
|**3004**|**adErrWriteFile**|寫入檔案失敗。 您可能已關閉檔案，然後嘗試寫入檔案，或檔案可能已損毀。 如果檔案位於網路磁碟機機上，暫時性的網路狀況可能會防止寫入網路磁碟機機。|
|**3021**|**adErrNoCurrentRecord**|**BOF**或**EOF**為 True，或目前的記錄已刪除。 要求的作業需要目前的記錄。<br /><br /> 嘗試使用 [ **尋找** ] 或 [ **搜尋** ] 將記錄指標移至所需的記錄，以更新記錄。 如果找不到記錄， **EOF** 將會是 True。 在失敗的 **AddNew** 或 **Delete** 之後，也可能會發生此錯誤，因為這些方法失敗時沒有目前的記錄。|
|**3219**|**adErrIllegalOperation**|此內容中不允許作業。|
|**3220**|**adErrCantChangeProvider**|提供的提供者與已在使用中的提供者不同。|
|**3246**|**adErrInTransaction**|在交易中，無法明確關閉**連接**物件。 目前參與交易的 **記錄集** 或 **連接** 物件無法關閉。 請在關閉物件之前呼叫 **RollbackTrans** 或 **CommitTrans** 。|
|**3251**|**adErrFeatureNotAvailable**|物件或提供者無法執行要求的作業。 某些作業相依于特定的提供者版本。|
|**3265**|**adErrItemNotFound**|在對應至所要求名稱或序數的集合中找不到專案。 指定了不正確的欄位或資料表名稱。|
|**3367**|**adErrObjectInCollection**|物件已經在集合中。 無法附加。 無法將物件加入至相同的集合兩次。|
|**3420**|**adErrObjectNotSet**|物件不再有效。|
|**3421**|**adErrDataConversion**|應用程式會針對目前的作業使用錯誤類型的值。 例如，您可能已提供字串給預期資料流程的作業。|
|**3704**|**adErrObjectClosed**|當物件關閉時，不允許作業。 **連接**或**記錄集**已關閉。 例如，某些其他常式可能已關閉全域物件。 您可以先檢查 **State** 屬性，然後再嘗試操作，以避免此錯誤。|
|**3705**|**adErrObjectOpen**|當物件開啟時，不允許作業。 無法開啟開啟的物件。 欄位不能附加至開啟的 **記錄集**。|
|**3706**|**adErrProviderNotFound**|找不到提供者。 可能未正確安裝。<br /><br /> 提供者的名稱可能不正確，指定的提供者可能不會安裝在執行您程式碼的電腦上，或者安裝可能已損毀。|
|**3707**|**adErrBoundToCommand**|無法變更**記錄集**物件的**ActiveConnection**屬性，其**命令**物件為其來源。 應用程式嘗試將新的**連接**物件指派給擁有**Command**物件做為其來源的**記錄集**。|
|**3708**|**adErrInvalidParamInfo**|**參數** 物件的定義不正確。 提供不一致或不完整的資訊。|
|**3709**|**adErrInvalidConnection**|無法使用連接來執行此作業。 在此內容中，它可能已關閉或無效。|
|**3710**|**adErrNotReentrant**|處理事件時，無法執行操作。 無法在造成事件再次引發的事件處理常式中執行作業。 例如，不應該從 **WillMove** 事件處理常式內呼叫流覽方法。|
|**3711**|**adErrStillExecuting**|以非同步方式執行時，無法執行操作。|
|**3712**|**adErrOperationCancelled**|使用者已取消作業。 應用程式已呼叫 **CancelUpdate** 或 **CancelBatch** 方法，且目前的作業已取消。|
|**3713**|**adErrStillConnecting**|非同步連接時無法執行操作。|
|**3714**|**adErrInvalidTransaction**|協調交易無效或尚未啟動。|
|**3715**|**adErrNotExecuting**|無法執行作業，但無法執行。|
|**3716**|**adErrUnsafeOperation**|這部電腦上的安全性設定禁止存取另一個網域上的資料來源。|
|**3717**|**adWrnSecurityDialog**|僅供內部使用。 請勿使用。 為了完整性，已包含 (專案。 此錯誤不應該出現在您的程式碼中。 ) |
|**3718**|**adWrnSecurityDialogHeader**|僅供內部使用。 請勿使用。 為了完整性而包含 (專案。 此錯誤不應該出現在您的程式碼中。 ) |
|**3719**|**adErrIntegrityViolation**|資料值與欄位的完整性條件約束衝突。 **欄位**的新值會導致重複的索引鍵。 形成兩筆記錄之間關聯性之一端的值可能不是可更新的。|
|**3720**|**adErrPermissionDenied**|許可權不足會防止寫入欄位。 連接字串中指定的使用者沒有適當的許可權可寫入 **欄位**。|
|**3721**|**adErrDataOverflow**|資料值太大，無法以欄位資料類型表示。 指派給預期欄位的數值太大。 例如，將長整數值指派給短整數位段。|
|**3722**|**adErrSchemaViolation**|資料值與欄位的資料類型或條件約束衝突。 資料存放區有不同于 **域** 值的驗證條件約束。|
|**3723**|**adErrSignMismatch**|轉換失敗，因為資料值已簽署，而提供者使用的欄位資料類型未簽署。|
|**3724**|**adErrCantConvertvalue**|由於符號不符或資料溢位以外的原因而無法轉換資料值。 例如，轉換會有截斷的資料。|
|**3725**|**adErrCantCreate**|無法設定或抓取資料值，因為欄位資料類型未知，或提供者沒有足夠的資源可執行作業。|
|**3726**|**adErrColumnNotOnThisRow**|記錄不包含此欄位。 指定了不正確的功能變數名稱，或參考了目前記錄之 **Fields** 集合中的欄位。|
|**3727**|**adErrURLDoesNotExist**|來源 URL 或目的地 URL 的父系不存在。 來源或目的地 URL 中有一種打字錯誤。 您可能會有 `https://mysite/photo/myphoto.jpg` 實際的時機 `https://mysite/photos/myphoto.jpg` 。 父 URL 中的打字錯誤 (在此案例中， *相片* 而非 *相片*) 導致錯誤。|
|**3728**|**adErrTreePermissionDenied**|許可權不足以存取樹狀結構或子樹。 連接字串中指定的使用者沒有適當的許可權。|
|**3729**|**adErrInvalidURL**|URL 包含不正確字元。 請確定 URL 的輸入是否正確。 URL 會遵循向目前提供者註冊的配置 (例如，為 HTTP) 註冊網際網路發佈提供者。|
|**3730**|**adErrResourceLocked**|由指定的 URL 表示的物件已被一或多個其他進程鎖定。 等候進程完成，然後再次嘗試操作。 您嘗試存取的物件已被另一個使用者或您應用程式中的另一個進程鎖定。 這最有可能發生在多使用者環境中。|
|**3731**|**adErrResourceExists**|無法執行複製作業。 目的地 URL 所命名的物件已經存在。 指定 **adCopyOverwrite** 來取代物件。 如果您在複製目錄中的檔案時未指定 **adCopyOverwrite** ，當您嘗試複製已存在於目的地位置的專案時，複製會失敗。|
|**3732**|**adErrCannotComplete**|伺服器無法完成操作。 這可能是因為伺服器正忙於處理其他作業，或是資源不足。|
|**3733**|**adErrVolumeNotFound**|提供者找不到 URL 所指出的儲存裝置。 請確定 URL 的輸入是否正確。 存放裝置的 URL 可能不正確，但由於其他原因，可能會發生此錯誤。 裝置可能已離線，或大量的網路流量可能會導致無法進行連接。|
|**3734**|**adErrOutOfSpace**|無法執行操作。 提供者無法取得足夠的儲存空間。 伺服器上的暫存檔案可能沒有足夠的 RAM 或硬碟空間。|
|**3735**|**adErrResourceOutOfScope**|來源或目的地 URL 超出目前記錄的範圍。|
|**3736**|**adErrUnavailable**|作業無法完成，且狀態為無法使用。 欄位可能無法使用，或未嘗試操作。 另一位使用者可能已變更或刪除您嘗試存取的欄位。|
|**3737**|**adErrURLNamedRowDoesNotExist**|這個 URL 所命名的記錄不存在。 嘗試使用 **記錄** 物件來開啟檔案時，檔案名或檔案的路徑拼錯。|
|**3738**|**adErrDelResOutOfScope**|要刪除之物件的 URL 超出目前記錄的範圍。|
|**3747**|**adErrCatalogNotSet**|作業需要有效的 **ParentCatalog**。|
|**3748**|**adErrCantChangeConnection**|連接遭到拒絕。 您所要求的新連接具有不同于已在使用中的連接特性。|
|**3749**|**adErrFieldsUpdateFailed**|欄位更新失敗。 如需詳細資訊，請檢查個別欄位物件的 **Status** 屬性。 在兩種情況下可能會發生此錯誤：在變更或加入記錄至資料庫的過程中變更 **欄位** 物件的值時：變更 **欄位** 物件本身的屬性。<br /><br /> **記錄**或**記錄集**更新失敗，因為目前記錄中的其中一個欄位發生問題。 列舉 **Fields** 集合，並檢查每個欄位的 **Status** 屬性，以判斷問題的原因。|
|**3750**|**adErrDenyNotSupported**|提供者不支援共用限制。 嘗試限制檔案共用，而您的提供者不支援此概念。|
|**3751**|**adErrDenyTypeNotSupported**|提供者不支援所要求的共用限制類型。 嘗試建立您的提供者不支援的特定檔共用限制類型。 請參閱提供者的檔，以判斷支援的檔案共用限制。|