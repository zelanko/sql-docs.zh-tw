---
title: "ADO 錯誤參考 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors [ADO], number reference
- errors [ADO], ErrorValueEnum
- ErrorValueEnum enumeration [ADO]
ms.assetid: f653393e-d4b0-4c34-ad5f-2bdf56bc1305
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2604f09ecffab3e0f5519731acffa00111af9677
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="ado-errors"></a>ADO 錯誤
**ErrorValueEnum**常數描述 ADO 錯誤值。 如需完整清單，這些列舉的常數，包括值，請參閱[附錄 b: ADO 錯誤](../../../ado/guide/appendixes/appendix-b-ado-errors.md)。 本章節將會檢查一些更有趣的錯誤，並說明某些特定情況下，或若要修正此問題的解決方案，可引發。 這兩個**ErrorValueEnum**列出常數和短正數的十進位數字。

|Number|ErrorValueEnum 常數|描述/可能的原因|
|------------|-----------------------------|----------------------------------|
|**3000**|**adErrProviderFailed**|提供者無法執行要求的作業。|
|**3001**|**adErrInvalidArgument**|引數的類型錯誤，超出可接受的範圍，或互相。 這個錯誤通常因 SQL SELECT 陳述式中的拼字錯誤。 例如，拼字錯誤的欄位名稱或資料表名稱可以產生這個錯誤。 當欄位或名為 SELECT 陳述式中的資料表不存在資料存放區中，也會發生這個錯誤。|
|**3002**|**adErrOpeningFile**|無法開啟檔案。 指定了拼字錯誤的檔案名稱，或將檔案移動、 重新命名或刪除。 在網路上的磁碟機可能是暫時無法使用或網路流量可能會無法連線。|
|**3003**|**adErrReadFile**|無法讀取檔案。 指定的檔案名稱不正確、 檔案可能已移動或刪除，或檔案可能已損毀。|
|**3004**|**adErrWriteFile**|寫入檔案失敗。 您可能已關閉檔案並再嘗試寫入其中，或檔案可能損毀。 如果檔案位於網路磁碟機上，暫時性的網路狀況可能會讓網路磁碟機的寫入。|
|**3021**|**adErrNoCurrentRecord**|任一**BOF**或**EOF**為 True，或目前的記錄已被刪除。 要求的作業需要目前的記錄。<br /><br /> 嘗試更新記錄使用**尋找**或**搜尋**記錄指標移動到需要的記錄。 如果找不到記錄， **EOF**會是 True。 也會發生此錯誤之後失敗**AddNew**或**刪除**因為無目前記錄時，這些方法都失敗。|
|**3219**|**adErrIllegalOperation**|在此內容中不允許作業。|
|**3220**|**adErrCantChangeProvider**|提供的提供者是不同的使用中。|
|**3246**|**adErrInTransaction**|**連接**物件無法在交易中明確地關閉。 A**資料錄集**或**連接**無法關閉目前參與交易的物件。 呼叫**RollbackTrans**或**CommitTrans**之前關閉物件。|
|**3251**|**adErrFeatureNotAvailable**|物件或提供者不支援執行要求的作業。 某些作業取決於特定提供者版本。|
|**3265**|**adErrItemNotFound**|無法在集合中找到項目，對應到要求的名稱或序數。 已指定正確的欄位或資料表名稱。|
|**3367**|**adErrObjectInCollection**|物件已經在集合中。 無法附加。 物件無法加入兩次相同的集合。|
|**3420**|**adErrObjectNotSet**|物件不再有效。|
|**3421**|**adErrDataConversion**|應用程式會使用目前的作業錯誤類型的值。 您可能會提供預期的資料流，例如作業的字串。|
|**3704**|**adErrObjectClosed**|當物件已關閉時，不允許作業。 **連接**或**資料錄集**已關閉。 例如，某些其他常式可能會關閉全域物件。 您可以檢查以避免這個錯誤**狀態**屬性才能嘗試進行作業。|
|**3705**|**adErrObjectOpen**|物件開啟時，不允許作業。 無法開啟已開啟的物件。 欄位不能附加至已開啟的**資料錄集**。|
|**3706**|**adErrProviderNotFound**|找不到提供者。 它可能不正確的安裝。<br /><br /> 可能未正確指定的提供者名稱，其中正在執行您的程式碼，或安裝已損毀的電腦上可能未安裝指定的提供者。|
|**3707**|**adErrBoundToCommand**|**ActiveConnection**屬性**資料錄集**，該物件具有**命令**作為其來源物件，無法變更。 應用程式已嘗試指派新**連接**物件**資料錄集**具有**命令**作為其來源的物件。|
|**3708**|**adErrInvalidParamInfo**|**參數**物件的定義不正確。 提供不一致或不完整的資訊。|
|**3709**|**adErrInvalidConnection**|連接無法用來執行這項作業。 它是已關閉，或在此內容中無效。|
|**3710**|**adErrNotReentrant**|正在處理事件時，無法執行作業。 無法執行作業，會再次引發事件的事件處理常式內。 例如，瀏覽方法不應該呼叫從**WillMove**事件處理常式。|
|**3711**|**adErrStillExecuting**|以非同步方式執行時，無法執行作業。|
|**3712**|**adErrOperationCancelled**|使用者已取消作業。 應用程式已呼叫**CancelUpdate**或**CancelBatch**方法和目前作業已取消。|
|**3713**|**adErrStillConnecting**|以非同步方式連線時，無法執行作業。|
|**3714**|**adErrInvalidTransaction**|協調交易無效或尚未啟動。|
|**3715**|**adErrNotExecuting**|未執行時，無法執行作業。|
|**3716**|**adErrUnsafeOperation**|在此電腦上的安全設定禁止存取另一個網域上的資料來源。|
|**3717**|**adWrnSecurityDialog**|僅供內部使用。 請勿使用。 （項目已包含為了完整起見。 這個錯誤應該不會出現在程式碼中。）|
|**3718**|**adWrnSecurityDialogHeader**|僅供內部使用。 請勿使用。 （項目包含為了完整起見。 這個錯誤應該不會出現在程式碼中。）|
|**3719**|**adErrIntegrityViolation**|資料值欄位的完整性條件約束衝突。 新值**欄位**會導致重複的索引鍵。 值，以構成兩筆記錄之間的關聯性的一端可能無法更新。|
|**3720**|**adErrPermissionDenied**|沒有足夠的權限可防止寫入的欄位。 名為連接字串中的使用者沒有適當的權限寫入**欄位**。|
|**3721**|**adErrDataOverflow**|資料值太大而無法表示欄位資料型別。 指派給預期的欄位太大的數值。 例如，一個長整數值已指派給短整數欄位。|
|**3722**|**adErrSchemaViolation**|資料值和資料類型或欄位的條件約束衝突。 資料存放區有不同的驗證條件約束**欄位**值。|
|**3723**|**adErrSignMismatch**|轉換失敗，因為資料值為 signed，而提供者所使用的欄位資料類型不帶正負號。|
|**3724**|**adErrCantConvertvalue**|由於符號不符或資料溢位以外的原因而無法轉換資料值。 例如，轉換會有截斷資料。|
|**3725**|**adErrCantCreate**|無法設定或擷取欄位資料型別為未知，或提供者有資源不足，無法執行作業，因為資料值。|
|**3726**|**adErrColumnNotOnThisRow**|記錄不包含此欄位。 指定了不正確的欄位名稱或欄位不能在**欄位**參考目前記錄的集合。|
|**3727**|**adErrURLDoesNotExist**|來源 URL 或目的地 URL 不存在的父系。 來源或目的地 URL 中沒有拼字錯誤。 您可能必須`http://mysite/photo/myphoto.jpg`時應該實際擁有`http://mysite/photos/myphoto.jpg`改為。 父 URL 中的印刷錯誤，(在此情況下，*相片*而不是*相片*) 造成錯誤。|
|**3728**|**adErrTreePermissionDenied**|權限還不足以存取樹狀目錄或樹狀子目錄。 名為連接字串中的使用者沒有適當的權限。|
|**3729**|**adErrInvalidURL**|URL 包含無效的字元。 請確定輸入的 URL 正確。 URL 會遵循向目前的提供者的配置 （例如，網際網路發行的提供者會登錄為 http）。|
|**3730**|**adErrResourceLocked**|指定的 URL 所代表的物件已鎖定一或多個其他處理程序。 請等候程序已完成，然後再次嘗試操作。 您嘗試存取的物件已被鎖定，由其他使用者或應用程式中的另一個處理序。 這是最有可能會發生在多使用者環境中。|
|**3731**|**adErrResourceExists**|無法執行複製作業。 物件名稱的目的地 URL 已經存在。 指定**adCopyOverwrite**取代物件。 如果您未指定**adCopyOverwrite**複製檔案的目錄中，當複製失敗時您嘗試複製已存在於目的地位置的項目。|
|**3732**|**adErrCannotComplete**|伺服器無法完成作業。 這可能是因為伺服器忙著處理其他作業，或可能是資源不足。|
|**3733**|**adErrVolumeNotFound**|提供者找不到安全的 URL 的存放裝置。 請確定輸入的 URL 正確。 存放裝置的 URL 可能不正確，但此錯誤可能是因為其他原因。 裝置可能是離線或大量的網路流量可能導致正在進行中的連接。|
|**3734**|**adErrOutOfSpace**|無法執行作業。 提供者無法取得足夠的儲存空間。 可能不會有足夠的 RAM 或伺服器上的暫存檔案的硬碟空間。|
|**3735**|**adErrResourceOutOfScope**|來源或目的地 URL 是記錄的在目前範圍之外。|
|**3736**|**adErrUnavailable**|無法完成操作，而無法使用狀態。 此欄位可能無法使用或不嘗試進行作業。 另一位使用者可能已變更或刪除您嘗試存取的欄位。|
|**3737**|**adErrURLNamedRowDoesNotExist**|此 URL 命名的記錄不存在。 嘗試開啟檔案使用時**記錄**物件、 檔案名稱或檔案的路徑已拼字錯誤。|
|**3738**|**adErrDelResOutOfScope**|要刪除之物件的 URL 是記錄的在目前範圍之外。|
|**3747**|**adErrCatalogNotSet**|作業需要有效**ParentCatalog**。|
|**3748**|**adErrCantChangeConnection**|已拒絕連線。 您要求新的連接會有不同的特性與已在使用中。|
|**3749**|**adErrFieldsUpdateFailed**|欄位更新失敗。 如需詳細資訊，請檢查**狀態**個別欄位物件的屬性。 兩種情況可能會發生此錯誤： 變更時**欄位**物件的值進行變更或新增一筆記錄，到資料庫; 以及變更的屬性時**欄位**物件本身。<br /><br /> **記錄**或**資料錄集**更新失敗，因為目前的記錄中欄位的其中一個問題。 列舉**欄位**集合，並檢查**狀態**屬性的每個欄位，以判斷問題的原因。|
|**3750**|**adErrDenyNotSupported**|提供者不支援共用限制。 嘗試將檔案共用，您的提供者不支援這個概念。|
|**3751**|**adErrDenyTypeNotSupported**|提供者不支援共用限制的要求的的類型。 嘗試建立特定類型的檔案共用您的提供者不支援的限制。 請參閱提供者的文件，以判斷支援哪些檔案共用限制。|

