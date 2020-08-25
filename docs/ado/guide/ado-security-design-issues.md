---
description: ADO 安全性設計功能
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a0ce44d1df589dc77a8a4cdfa216b0c54ce288dc
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805478"
---
# <a name="ado-security-design-features"></a>ADO 安全性設計功能
下列章節說明 ActiveX Data Objects (ADO) 2.8 和更新版本中的安全性設計功能。 這些變更已在 ADO 2.8 中進行，以提升安全性。 Windows Vista 中的 Windows DAC 6.0 中包含的 ADO 6.0，在功能上相當於 Windows XP 和 Windows Server 2003 中的 MDAC 2.8 所包含的 ADO 2.8。 本主題提供有關如何在 ADO 2.8 或更新版本中最安全地保護應用程式的資訊。

> [!IMPORTANT]
>  如果您要從舊版 ADO 更新您的應用程式，建議您先在非生產電腦上測試更新的應用程式，再將它部署至客戶。 如此一來，您可以在部署更新的應用程式之前，確定您知道是否有任何相容性問題。

## <a name="internet-explorer-file-access-scenarios"></a>Internet Explorer 檔案存取案例
 當 ADO 2.8 和更新版本在 Internet Explorer 的腳本網頁中使用時，下列功能會生效。

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>修訂和改進的安全性警告訊息框現在可用來警示使用者
 針對 ADO 2.7 及更早版本，當腳本的網頁嘗試從未受信任的提供者執行 ADO 程式碼時，會出現下列警告訊息：

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

 上述訊息可讓使用者做出明智的決策，同時瞭解任一選擇的後果：

-   如果使用者信任網站，按一下 [確定] 將會允許所有的磁片安全程式碼 (所有 ADO 方法和屬性，但本主題稍後所述的可存取磁片的 Api 例外) 在瀏覽器視窗中執行和執行。

-   如果使用者不信任網站，則按一下 [取消] 會封鎖 ADO 程式碼，讓資料存取無法執行並完整執行。

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>磁片可存取的程式碼現已限制為信任的網站
 ADO 2.8 中的其他設計變更是特別限制一組有限 Api 的能力，而這可能會造成在本機電腦上讀取或寫入檔案的可能性。 以下是執行 Internet Explorer 時，已針對安全而進一步限制的 API 方法：

-   如果使用[LoadFromFile](../reference/ado-api/loadfromfile-method-ado.md)或[SaveToFile](../reference/ado-api/savetofile-method.md)方法，則適用于 ADO**資料流程**物件。

-   如果是 ADO **記錄集** 物件，請使用 [Save](../reference/ado-api/save-method.md) 方法或 [Open](../reference/ado-api/open-method-ado-recordset.md) 方法（例如，在設定 **AdCmdFile** 選項時），或使用 [Microsoft OLE DB 持續性提供者 (MSPersist) ](./appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) 。

 針對這些有限的可能磁片可存取函式集合，如果有任何使用這些方法的程式碼在 Internet Explorer 中執行，則 ADO 2.8 和更新版本會發生下列行為：

-   如果提供程式碼的網站先前已新增至 [信任的網站] 區域清單，程式碼就會在瀏覽器中執行，並將存取權授與本機檔案。

-   如果網站未出現在 [信任的網站] 區域清單中，則會封鎖程式碼並拒絕存取本機檔案。

    > [!NOTE]
    >  在 ADO 2.8 和更新版本中，使用者不會收到警示或建議將網站新增至 [信任的網站] 區域清單。 因此，管理受信任的網站清單，是要部署或支援需要存取本機檔案系統的網站架構應用程式之人員的責任。

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>對記錄集物件的 ActiveCommand 屬性封鎖存取
 在 Internet Explorer 中執行時，ADO 2.8 現在會封鎖對使用中**記錄集**物件的[ActiveCommand](../reference/ado-api/activecommand-property-ado.md)屬性存取，並傳回錯誤。 無論頁面是否來自 [信任的網站] 清單中註冊的網站，都會發生此錯誤。

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>OLE DB 提供者和整合式安全性的處理變更
 針對潛在的安全性問題和考慮，查看 ADO 2.7 和較早的版本時，已發現下列案例：

 在某些情況下，支援整合式安全性 [DBPROP_AUTH_INTEGRATED](/previous-versions/windows/desktop/ms712973(v=vs.85)) 屬性的 OLE DB 提供者可能會允許已編寫腳本的網頁重複使用 ADO 連線物件，以使用使用者目前的登入認證，不慎連接到其他伺服器。 為了避免發生這種情況，ADO 2.8 和更新版本會根據其選擇提供（或不提供）整合式安全性的方式，來處理 OLE DB 提供者。

 針對從 [信任的網站] 區域清單中列出的網站載入的網頁，下表提供 ADO 2.8 和更新版本如何在每個案例中管理 ADO 連接的明細。

|使用者驗證的 IE 設定，登入|提供者支援「整合式安全性」，而且 UID 和 PWD (SQLOLEDB 指定) |提供者不支援「整合式安全性」 (JOLT、MSDASQL、MSPersist) |提供者支援「整合式安全性」，且設定為 SSPI (未指定任何 UID/PWD) |
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|使用目前的使用者名稱和密碼自動登入|允許連線|允許連線|允許連線|
|提示輸入使用者名稱和密碼|允許連線|連接失敗|連接失敗|
|只在內部網路區域自動登入|允許連線|提示使用者出現安全性警告|提示使用者出現安全性警告|
|匿名登入|允許連線|連接失敗|連接失敗|

 在現在出現安全性警告的情況下，訊息方塊會通知使用者：

```console
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 上述訊息可讓使用者做出更明智的決策，並據以繼續。

> [!NOTE]
>  針對未受信任的網站 (也就是未列在 [信任的網站] 區域清單中的網站) ，如果提供者也不受信任 (如本節稍早所述) ，則使用者可能會在資料列中看到兩個安全性警告，這是有關不安全提供者的警告，以及嘗試使用其身分識別的第二個警告。 如果使用者按一下 [確定] 第一個警告，則會執行上表所述的 Internet Explorer 設定和回應行為程式碼。

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>控制是否要在 ADO 連接字串中傳回密碼文字
 當您嘗試取得 ADO**連接**物件的[ConnectionString](../reference/ado-api/connectionstring-property-ado.md)屬性值時，會發生下列事件：

1.  如果連接已開啟，則會對基礎 OLE DB 提供者進行初始化呼叫，以取得連接字串。

2.  根據 [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](/previous-versions/windows/desktop/ms714905(v=vs.85)) 屬性之 OLE DB 提供者中的設定，密碼會與傳回的其他連接字串資訊一起包含在一起。

 例如，如果 ADO 連接動態屬性 **保存安全性資訊** 設為 **True**，則會在傳回的連接字串中包含密碼資訊。 否則，如果基礎提供者已將此屬性設定為 **False** (例如使用 SQLOLEDB 提供者) ，則會在傳回的連接字串中省略密碼資訊。

 如果您使用的是協力廠商 (，也就是您的 ADO 應用程式程式碼中的非 Microsoft) OLE DB 提供者，您可能會檢查 **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO** 屬性的執行方式，以判斷是否允許在 ado 連接字串中包含密碼資訊。

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>在載入和儲存記錄集或資料流程時檢查非檔案裝置
 針對 ADO 2.7 及更早版本，用來讀取和寫入以檔案為基礎之資料的檔案輸入/輸出作業（例如 [ [開啟](../reference/ado-api/open-method-ado-recordset.md) ] 和 [ [儲存](../reference/ado-api/save-method.md) ]）在某些情況下可能會允許使用指定非磁片型檔案類型的 URL 或檔案名。 例如，您可以使用 LPT1、COM2、PRN.TXT、AUX 作為系統上的印表機和輔助裝置之間的輸入/輸出別名（使用特定的

 針對 ADO 2.8 和更新版本，此功能已更新。 針對開啟和儲存 **記錄集** 和 **資料流程** 物件，ADO 現在會執行檔案類型檢查，以確保 URL 或檔案名中指定的輸入或輸出裝置是實際的檔案。

> [!NOTE]
>  本章節所述的檔案類型檢查只適用于 Windows 2000 和更新版本。 這不適用於 ADO 2.8 或更新版本在舊版 Windows （例如 Windows 98）下執行的情況。