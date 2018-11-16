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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a71b651df387bfe28992d426fd2080587e439ad
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600918"
---
# <a name="ado-errors"></a>ADO 錯誤
**ErrorValueEnum**常數描述 ADO 錯誤值。 如需完整清單，這些列舉的常數，包括值，請參閱[附錄 b: ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)。 本節會檢查一些更有趣的錯誤，並說明某些特定的情況下，可能會引發，或若要修正此問題的解決方案。 這兩個**ErrorValueEnum**列出常數及簡短的正面十進位數字。

|Number|ErrorValueEnum 常數|描述/可能的原因|
|------------|-----------------------------|----------------------------------|
|**3000**|**adErrProviderFailed**|提供者無法執行要求的作業。|
|**3001**|**adErrInvalidArgument**|引數的類型錯誤，超出可接受的範圍，或與彼此衝突。 此錯誤通常因 SQL SELECT 陳述式中發生打字錯誤。 比方說，拼字錯誤的欄位名稱或資料表名稱可能會產生此錯誤。 欄位或 SELECT 陳述式中所命名的資料表不存在於資料存放區時，也會發生此錯誤。|
|**3002**|**adErrOpeningFile**|無法開啟檔案。 指定的拼字錯誤的檔案名稱，或將檔案移動、 重新命名或刪除。 在網路上的磁碟機可能會暫時無法使用，或網路流量可能會無法連線。|
|**3003**|**adErrReadFile**|無法讀取檔案。 不正確地指定檔案的名稱、 檔案可能已移動或刪除，或該檔案可能已損毀。|
|**3004**|**adErrWriteFile**|寫入檔案失敗。 您可能已關閉檔案，並嘗試寫入其中，或者檔案可能損毀。 如果該檔案位於網路磁碟機，暫時性的網路狀況可能會讓寫入至網路磁碟機。|
|**3021**|**adErrNoCurrentRecord**|任一**BOF**或是**EOF**為 True，或已刪除目前的記錄。 要求的作業需要目前的記錄。<br /><br /> 嘗試使用更新資料錄**尋找**或**搜尋**將記錄指標移至所需的記錄。 如果找不到記錄， **EOF**會是 True。 也會發生此錯誤之後失敗**AddNew**或是**刪除**因為沒有目前資料錄時，這些方法都失敗。|
|**3219**|**adErrIllegalOperation**|在此內容中不允許作業。|
|**3220**|**adErrCantChangeProvider**|提供的提供者是不同於已在使用中。|
|**3246**|**adErrInTransaction**|**連接**物件無法在交易中明確地關閉。 A **Recordset**或是**連線**目前參與交易的物件，所以無法關閉。 呼叫**RollbackTrans**或是**CommitTrans**之前關閉物件。|
|**3251**|**adErrFeatureNotAvailable**|物件或提供者不支援執行要求的作業。 某些作業取決於特定提供者版本。|
|**3265**|**adErrItemNotFound**|無法在集合中找到項目，對應到要求的名稱或序數。 已指定正確的欄位或資料表名稱。|
|**3367**|**adErrObjectInCollection**|物件已經在集合中。 無法附加。 物件無法加入兩次相同的集合。|
|**3420**|**adErrObjectNotSet**|物件不再有效。|
|**3421**|**adErrDataConversion**|應用程式會使用目前的操作錯誤類型的值。 您可能會提供預期的資料流，例如作業的字串。|
|**3704**|**adErrObjectClosed**|當物件已關閉時，不允許作業。 **連接**或是**資料錄集**已關閉。 比方說，某些其他常式可能已關閉的全域物件。 您可以藉由檢查來避免此錯誤**狀態**才能嘗試進行作業的屬性。|
|**3705**|**adErrObjectOpen**|開啟物件時，不允許作業。 無法開啟已開啟的物件。 欄位不能附加至開放**資料錄集**。|
|**3706**|**adErrProviderNotFound**|找不到提供者。 它可能不正確的安裝。<br /><br /> 提供者的名稱可能不正確地指定，其中正在執行您的程式碼，或安裝可能已損毀的電腦上可能未安裝指定的提供者。|
|**3707**|**adErrBoundToCommand**|**ActiveConnection**屬性**Recordset**物件，其中包含**命令**物件做為其來源，無法變更。 應用程式已嘗試指派的新**連接**物件**資料錄集**具有**命令**做為其來源的物件。|
|**3708**|**adErrInvalidParamInfo**|**參數**物件的定義不正確。 提供不一致或不完整的資訊。|
|**3709**|**adErrInvalidConnection**|連接不用來執行這項作業。 它會關閉，或在此內容中無效。|
|**3710**|**adErrNotReentrant**|在處理事件時，無法執行作業。 無法執行作業，會導致再次引發事件的事件處理常式內。 比方說，瀏覽方法不應該呼叫內在**WillMove**事件處理常式。|
|**3711**|**adErrStillExecuting**|以非同步方式執行時，無法執行作業。|
|**3712**|**adErrOperationCancelled**|已由使用者取消作業。 應用程式已呼叫**CancelUpdate**或是**CancelBatch**方法和目前的作業已取消。|
|**3713**|**adErrStillConnecting**|以非同步方式連線時，無法執行作業。|
|**3714**|**adErrInvalidTransaction**|協調交易無效，或尚未啟動。|
|**3715**|**adErrNotExecuting**|未執行時，無法執行作業。|
|**3716**|**adErrUnsafeOperation**|在此電腦上的安全設定禁止存取另一個網域上的資料來源。|
|**3717**|**adWrnSecurityDialog**|僅供內部使用。 請勿使用。 （項目是包含為了完整起見。 這個錯誤應該不會出現在您的程式碼。）|
|**3718**|**adWrnSecurityDialogHeader**|僅供內部使用。 請勿使用。 （為了完整起見所包含的項目。 這個錯誤應該不會出現在您的程式碼。）|
|**3719**|**adErrIntegrityViolation**|資料值欄位的完整性條件約束的衝突。 新的值給**欄位**會導致重複的索引鍵。 值，會形成兩個記錄之間的關聯性的一端可能無法更新。|
|**3720**|**adErrPermissionDenied**|沒有足夠的權限可防止寫入至欄位。 名為連接字串中的使用者沒有寫入適當的權限**欄位**。|
|**3721**|**adErrDataOverflow**|資料值太大而無法欄位資料型別所表示。 已指派為預期的欄位太大的數值。 例如，一個長整數值已指派給短整數欄位。|
|**3722**|**adErrSchemaViolation**|資料值和資料型別或欄位的條件約束的衝突。 資料存放區有與不同的驗證條件約束**欄位**值。|
|**3723**|**adErrSignMismatch**|轉換失敗，因為資料值已簽署，且提供者所使用的欄位資料類型不帶正負號。|
|**3724**|**adErrCantConvertvalue**|由於符號不符或資料溢位以外的原因，無法轉換資料值。 例如，轉換會有截斷的資料。|
|**3725**|**adErrCantCreate**|無法設定或擷取欄位資料類型是未知，或提供者有資源不足，無法執行作業，因為資料值。|
|**3726**|**adErrColumnNotOnThisRow**|記錄不包含此欄位。 指定了不正確的欄位名稱或欄位不是位於**欄位**參考目前資料錄的集合。|
|**3727**|**adErrURLDoesNotExist**|來源 URL 或父項目的 URL 不存在。 在來源或目的地的 URL 中沒有錯字。 您可能會有`https://mysite/photo/myphoto.jpg`當您應該實際擁有`https://mysite/photos/myphoto.jpg`改。 父 URL 中的印刷錯誤，(在此情況下，*相片*而不是*相片*) 造成錯誤。|
|**3728**|**adErrTreePermissionDenied**|權限還不足以存取樹狀目錄或樹狀子目錄。 名為連接字串中的使用者沒有適當的權限。|
|**3729**|**adErrInvalidURL**|URL 包含無效的字元。 請確定輸入的 URL 正確。 URL 遵循註冊到目前的提供者的配置 （例如 http 為登錄網際網路發行的提供者）。|
|**3730**|**adErrResourceLocked**|所指定的 URL 表示的物件已鎖定的一或多個其他處理序。 請等候程序已完成，然後再次嘗試操作。 您嘗試存取的物件已被鎖定，由另一個使用者或應用程式中的另一個處理序。 這是最有可能發生在多使用者環境中。|
|**3731**|**adErrResourceExists**|無法執行複製作業。 物件名稱的目的地 URL 已經存在。 指定**adCopyOverwrite**來取代物件。 如果您未指定**adCopyOverwrite**時複製檔案的目錄中，複製失敗時您嘗試複製已存在於目的地位置的項目。|
|**3732**|**adErrCannotComplete**|伺服器無法完成作業。 這可能是因為伺服器忙著處理其他作業，或可能是資源不足。|
|**3733**|**adErrVolumeNotFound**|提供者找不到由 URL 的存放裝置。 請確定輸入的 URL 正確。 存放裝置的 URL 可能不正確，但基於其他原因會發生此錯誤。 裝置可能是離線或大量的網路流量可能會導致進行連線。|
|**3734**|**adErrOutOfSpace**|無法執行作業。 提供者無法取得足夠的儲存空間。 可能不會有足夠的 RAM 或伺服器上的暫存檔案的硬碟空間。|
|**3735**|**adErrResourceOutOfScope**|來源或目的地的 URL 是記錄的在目前範圍之外。|
|**3736**|**adErrUnavailable**|作業無法完成，且狀態為無法使用。 這個欄位可能是無法使用或未嘗試此作業。 另一位使用者可能會有變更或刪除您嘗試存取的欄位。|
|**3737**|**adErrURLNamedRowDoesNotExist**|此 URL 命名的記錄不存在。 嘗試開啟檔案時**記錄**物件時，檔案名稱或檔案的路徑是拼字錯誤。|
|**3738**|**adErrDelResOutOfScope**|要刪除之物件的 URL 是記錄的在目前範圍之外。|
|**3747**|**adErrCatalogNotSet**|作業需要有效**ParentCatalog**。|
|**3748**|**adErrCantChangeConnection**|連線被拒。 您要求新的連接都有高於已在使用中的不同特性。|
|**3749**|**adErrFieldsUpdateFailed**|欄位更新失敗。 如需詳細資訊，請檢查**狀態**個別欄位物件的屬性。 有兩種情況可能會發生此錯誤： 變更**欄位**物件的值，在過程中變更或新增記錄至資料庫; 以及變更的屬性時**欄位**物件本身。<br /><br /> **記錄**或是**資料錄集**更新失敗，發生問題的其中一個是目前記錄中欄位。 列舉**欄位**集合，並檢查**狀態**屬性的每個欄位，以判斷問題的原因。|
|**3750**|**adErrDenyNotSupported**|提供者不支援共用的限制。 嘗試將檔案共用的限制，您的提供者不支援的概念。|
|**3751**|**adErrDenyTypeNotSupported**|提供者不支援共用限制的要求的的類型。 嘗試建立特定類型的檔案共用您的提供者不支援的限制。 請參閱提供者的文件，以判斷支援哪些檔案共用的限制。|
