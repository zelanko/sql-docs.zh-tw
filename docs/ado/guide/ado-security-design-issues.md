---
title: ADO 安全性設計問題 |Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f638f6e48dccccd91849f02c65331d9212f9bbb7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67927031"
---
# <a name="ado-security-design-features"></a>ADO 安全性設計功能
下列各節說明 ActiveX Data Objects （ADO）2.8 和更新版本中的安全性設計功能。 這些變更是在 ADO 2.8 中進行，以改善安全性。 在 windows Vista 中，Windows DAC 6.0 隨附的 ADO 6.0 功能相當於 ADO 2.8，其隨附于 Windows XP 和 Windows Server 2003 的 MDAC 2.8 中。 本主題提供如何在 ADO 2.8 或更新版本中以最佳方式保護應用程式的相關資訊。

> [!IMPORTANT]
>  如果您要從舊版 ADO 更新應用程式，建議您先在非生產電腦上測試更新的應用程式，再將它部署給客戶。 如此一來，您就可以在部署更新的應用程式之前，確保您知道是否有任何相容性問題。

## <a name="internet-explorer-file-access-scenarios"></a>Internet Explorer 檔案存取案例
 下列功能會影響 ADO 2.8 和更新版本在 Internet Explorer 的腳本 Web 網頁中使用時的運作方式。

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>已修訂並改良安全性警告訊息框，現已用來警示使用者
 針對 ADO 2.7 和更早版本，當已編寫腳本的網頁嘗試從不受信任的提供者執行 ADO 程式碼時，會出現下列警告訊息：

```console
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 若為 ADO 2.8 和更新版本，則不會再出現上述訊息。 相反地，下列訊息會出現在此內容中：

```console
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 上述訊息可讓使用者做出明智的決策，同時瞭解任一選擇的結果：

-   如果使用者信任此網站，按一下 [確定] 將允許所有的磁片安全程式碼（所有 ADO 方法和屬性，其中包含本主題稍後所述的磁片可存取 Api 除外），以在瀏覽器視窗中執行並執行。

-   如果使用者不信任此網站，按一下 [取消] 會封鎖 ADO 程式碼，讓資料存取無法執行並在整個中執行。

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>可存取磁片的程式碼現在限制為信任的網站
 ADO 2.8 中進行了其他設計變更，特別限制一組有限的 Api，這可能會讓您無法讀取或寫入本機電腦上的檔案。 以下是在執行 Internet Explorer 時，針對安全而進一步限制的 API 方法：

-   如果使用[LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md)或[SaveToFile](../../ado/reference/ado-api/savetofile-method.md)方法，則為 ADO**資料流程**物件。

-   若是 ADO**記錄集**物件，則為，如果使用[Save](../../ado/reference/ado-api/save-method.md)方法或[Open](../../ado/reference/ado-api/open-method-ado-recordset.md)方法（例如設定了**AdCmdFile**選項時），或使用[Microsoft OLE DB 持續性提供者（MSPersist）](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) ，則為。

 針對這些有限的可能磁片可存取函式集合，如果使用這些方法的任何程式碼是在 Internet Explorer 中執行，則 ADO 2.8 和更新版本會發生下列行為：

-   如果提供程式碼的網站先前已新增到 [信任的網站] 區域清單中，則程式碼會在瀏覽器中執行，並將存取權授與本機檔案。

-   如果網站未出現在 [信任的網站] 區域清單中，則會封鎖程式碼，並拒絕存取本機檔案。

    > [!NOTE]
    >  在 ADO 2.8 和更新版本中，使用者不會收到警示或建議將網站新增至 [信任的網站] 區域清單。 因此，信任的網站清單的管理是負責部署或支援需要存取本機檔案系統之網站應用程式的人員。

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>封鎖存取記錄集物件上的 ActiveCommand 屬性
 在 Internet Explorer 中執行時，ADO 2.8 現在會封鎖 active **Recordset**物件的[ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md)屬性存取，並傳回錯誤。 不論頁面是否來自 [信任的網站] 清單中註冊的網站，都會發生此錯誤。

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>OLE DB 提供者和整合式安全性的處理變更
 在查看 ADO 2.7 和更早版本，以瞭解潛在的安全性問題和考慮時，會發現下列案例：

 在某些情況下，支援「整合式安全性[DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx) 」屬性的 OLE DB 提供者可能會允許腳本的網頁重複使用 ADO Connection 物件，以不小心地連接到使用使用者目前登入認證的其他伺服器。 為了避免這種情況，ADO 2.8 和更新版本會根據其選擇為整合式安全性提供或不提供的方式，來處理 OLE DB 提供者。

 針對從 [信任的網站] 區域清單中所列的網站載入的網頁，下表提供 ADO 2.8 和更新版本在每個案例中如何管理 ADO 連接的細目。

|使用者驗證、登入的 IE 設定|提供者支援「整合式安全性」，並已指定 UID 和 PWD （SQLOLEDB）|提供者不支援「整合式安全性」（JOLT、MSDASQL、MSPersist）|提供者支援「整合式安全性」，並設定為 SSPI （未指定 UID/PWD）|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|使用目前的使用者名稱和密碼自動登入|允許連線|允許連線|允許連線|
|提示輸入使用者名稱和密碼|允許連線|連接失敗|連接失敗|
|只在內部網路區域自動登入|允許連線|提示使用者安全性警告|提示使用者安全性警告|
|匿名登入|允許連線|連接失敗|連接失敗|

 在現在出現安全性警告的情況下，訊息方塊會通知使用者：

```console
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 先前的訊息可讓使用者做出更明智的決策，並據此繼續進行。

> [!NOTE]
>  針對不受信任的網站（也就是未列在 [信任的網站] 區域清單中的網站），如果提供者也不受信任（如本節稍早所述），則使用者可能會在資料列中看到兩個安全性警告、不安全提供者的警告，以及有關的第二個警告。嘗試使用其身分識別。 如果使用者在第一個警告中按一下 [確定]，則會執行上表中所述的 Internet Explorer 設定和回應行為程式碼。

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>控制是否要在 ADO 連接字串中傳回密碼文字
 當您嘗試取得 ADO**連接**物件的[ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md)屬性值時，會發生下列事件：

1.  如果連接已開啟，則會接著對基礎 OLE DB 提供者進行初始化呼叫，以取得連接字串。

2.  視[DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx)屬性的 OLE DB 提供者中的設定而定，密碼會連同傳回的其他連接字串資訊一起包含在一起。

 例如，如果「ADO 連接動態屬性」**保存安全性資訊**設定為**True**，則密碼資訊會包含在傳回的連接字串中。 否則，如果基礎提供者已將屬性設定為**False** （例如使用 SQLOLEDB 提供者），則會在傳回的連接字串中省略密碼資訊。

 如果您使用協力廠商（亦即非 Microsoft） OLE DB 提供者與您的 ADO 應用程式代碼，您可能會檢查如何執行**DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO**屬性，以判斷是否允許使用 ado 連接字串來包含密碼資訊。

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>載入和儲存記錄集或資料流程時檢查非檔案裝置
 針對 ADO 2.7 和更早版本，檔案輸入/輸出作業（例如，用來讀取和寫入以檔案為基礎之資料的[開啟](../../ado/reference/ado-api/open-method-ado-recordset.md)和[儲存](../../ado/reference/ado-api/save-method.md)）可能會允許使用 URL 或檔案名來指定非磁片型的檔案類型。 例如，LPT1、COM2、PRN。TXT，AUX 可用來做為印表機與系統上的輔助裝置之間的輸入/輸出別名（使用特定的

 針對 ADO 2.8 和更新版本，這是已更新的功能。 針對開啟和儲存**記錄集**和**資料流程**物件，ADO 現在會執行檔案類型檢查，以確保 URL 或檔案名中指定的輸入或輸出裝置是實際的檔案。

> [!NOTE]
>  這一節中所述的檔案類型檢查僅適用于 Windows 2000 和更新版本。 這不適用於在舊版 Windows （例如 Windows 98）下執行 ADO 2.8 或更新版本的情況。
