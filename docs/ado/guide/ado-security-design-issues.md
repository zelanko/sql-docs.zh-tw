---
title: "ADO 安全性設計問題 |Microsoft 文件"
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.technology: "“drivers”"
ms.topic: article
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 51c7e3cf9c99bdd76ce1b84a7c387b1e6e4d2f58
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="ado-security-design-features"></a>ADO 安全性設計功能
下列各節會說明安全性設計功能中 ActiveX Data Objects (ADO) 2.8 和更新版本。 在 ADO 中 2.8 已進行這些變更，以提升安全性。 ADO 6.0 中，隨附於 Windows Vista 中的 Windows DAC 6.0，在功能上等於 ADO 2.8，包含在 Windows XP 和 Windows Server 2003 中的 MDAC 2.8 中。 本主題提供如何最安全的 ADO 2.8 或更新版本中的您應用程式的相關資訊。

> [!IMPORTANT]
>  如果您要更新您的應用程式從 ADO 的較早版本，建議您測試在非實際執行電腦上的應用程式更新，然後再部署給客戶。 如此一來，您可以確保您部署應用程式更新之前，您可辨識的任何相容性問題。

## <a name="internet-explorer-file-access-scenarios"></a>Internet Explorer 檔案存取案例
 下列功能結果中使用時，ADO 2.8 和更新版本的運作方式編寫指令碼在 Internet Explorer 的網頁。

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>現在使用來警示使用者修訂和改善的安全性警告訊息方塊
 ADO 2.7 及更早版本中，針對已編寫指令碼的網頁嘗試執行不受信任的提供者的 ADO 程式碼時，會出現下列警告訊息：

```
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 ADO 2.8 和更新版本中，如先前的訊息不會再出現。 相反地，在此內容中出現下列訊息：

```
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 先前的訊息可讓使用者以進行明智的決策，同時在任一個選擇結果：

-   如果使用者信任的網站，按一下 [確定] 可讓所有的磁碟安全程式碼 （所有的 ADO 方法和屬性，與本主題稍後所述的磁碟存取 api 的例外狀況） 執行，並在瀏覽器視窗中執行。

-   如果使用者不信任的網站，請按一下 取消封鎖 ADO 程式碼的執行，以及執行完整的資料存取。

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>磁碟可存取的程式碼現在受限於信任的網站
 在 ADO 中特別限制一組有限的 Api，可能會公開可能會讀取或寫入至本機電腦上檔案的能力的 2.8 發生其他設計變更。 以下是 API 方法已進一步執行 Internet Explorer 時，安全的限制：

-   用於 ADO**資料流**物件，如果[LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md)或[SaveToFile](../../ado/reference/ado-api/savetofile-method.md)使用的方法。

-   用於 ADO**資料錄集**物件，如果有任一個[儲存](../../ado/reference/ado-api/save-method.md)方法或[開啟](../../ado/reference/ado-api/open-method-ado-recordset.md)方法，例如當任一**adCmdFile**選項會設定或[Microsoft OLE DB 持續性提供者 (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)用。

 這些有限的潛在磁碟存取函式，如下列的行為便會發生 ADO 2.8 和更新版本，如果使用這些方法的任何程式碼在 Internet Explorer 中執行：

-   如果提供的程式碼的站台之前已新增至信任的網站區域清單，在瀏覽器中執行的程式碼和存取權授與本機檔案。

-   如果網站不會出現在信任的網站區域清單中，程式碼會封鎖，並拒絕存取本機檔案。

    > [!NOTE]
    >  在 ADO 2.8 和更新版本中，使用者未收到警示或建議將網站新增到信任的網站區域清單。 因此信任的網站清單的管理是要部署或網站為基礎的應用程式需要存取本機檔案系統的支援人員的責任。

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>資料錄集物件的 ActiveCommand 內容封鎖存取
 Internet Explorer 中執行時，ADO 2.8 現在會封鎖存取[ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md)作用中的屬性**資料錄集**物件，並傳回錯誤。 不論頁面是否來自信任的網站清單中註冊的網站，就會發生錯誤。

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>在處理中的 OLE DB 提供者和整合式的安全性的變更
 檢視 ADO 2.7 和舊版的潛在安全性問題和考量，時發現下列案例：

 在某些情況下，OLE DB 提供者支援整合式安全性[DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx)屬性可能會允許執行指令碼的網頁以重複使用 ADO 連接物件不小心連接到其他伺服器使用目前登入認證的使用者。 若要防止這個情況，ADO 2.8 和更新版本會處理依據所選的方式提供，或未提供的整合式安全性的 OLE DB 提供者。

 從信任的網站區域的清單中列出的站台會載入的網頁下, 表提供細目 ADO 2.8 和更新版本管理每個案例中的 ADO 連接的方式。

|使用者驗證，IE 設定登入|提供者會支援 「 整合式安全性 」 及 UID 和 PWD 被指定 (SQLOLEDB)|提供者不支援 「 整合式安全性 」 的 (JOLT，MSDASQL，MSPersist)|提供者支援 「 整合式安全性 」，並會設為 SSPI （指定沒有 UID/PWD）|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|使用目前的使用者名稱和密碼自動登入|允許連線|允許連線|允許連線|
|提示輸入使用者名稱和密碼|允許連線|連接失敗|連接失敗|
|只在近端內部網路區域自動登入|允許連線|提示使用者安全性警告|提示使用者安全性警告|
|匿名登入|允許連線|連接失敗|連接失敗|

 安全性警告現在出現位置的情況下，訊息方塊會通知使用者：

```
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 先前的訊息可讓使用者做出更明智的決策，並視情況繼續執行。

> [!NOTE]
>  針對受信任的網站 （也就是網站信任的網站區域清單中未列出），如果提供者也不受信任 （如本節稍早所述），使用者可能會看到資料列、 不安全的提供者的相關警告和第二個警告中的兩個安全性警告嘗試使用其身分識別。 如果使用者按一下 [確定] 的第一個警告，就會執行的 Internet Explorer 設定和回應行為的程式碼在上表中所述。

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>控制 ADO 連接字串中是否傳回密碼文字
 當您嘗試取得的值[ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md)屬性 ADO**連接**物件時，發生下列事件：

1.  如果連接為開啟，初始化是然後撥打至基礎 OLE DB 提供者以取得連接字串。

2.  根據 OLE DB 提供者中的設定[DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx)屬性，密碼是包含傳回的其他連接字串資訊。

 例如，如果 ADO 連接的動態屬性**Persist Security Info**設為**True**，傳回的連接字串中包含密碼資訊。 否則，如果基礎提供者已將屬性設定為**False** （例如使用 SQLOLEDB 提供者），傳回的連接字串中省略密碼資訊。

 如果您使用協力廠商 (亦即，非 Microsoft) 搭配 ADO 的應用程式程式碼的 OLE DB 提供者，您可以檢查如何**DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO**屬性實作程序來判斷是否包含允許使用 ADO 連接字串的密碼資訊。

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>檢查非檔案裝置時載入及儲存資料錄集或資料流
 ADO 2.7 及更早版本中，為檔案輸入/輸出作業例如[開啟](../../ado/reference/ado-api/open-method-ado-recordset.md)和[儲存](../../ado/reference/ado-api/save-method.md)用來讀取和寫入檔案為基礎的資料可能在某些情況下允許的 URL 或檔案名稱來指定非磁碟根據檔案類型。 例如，LPT1、 COM2、 PRN。TXT、 AUX 可用於做為別名印表機與輔助裝置之間系統使用特定的輸入/輸出

 已更新為 ADO 2.8 和更新版本中，這項功能。 開啟和儲存**資料錄集**和**資料流**物件 ADO 立即執行檔案類型檢查，以確認 URL 或檔案名稱中指定的輸入或輸出裝置的實際檔案。

> [!NOTE]
>  檔案類型檢查這一節中所述僅適用於 Windows 2000 和更新版本。 它不適用於 ADO 2.8 或更新版本，執行較早的 Windows 版本，例如 Windows 98 的情況。

