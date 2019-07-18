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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927031"
---
# <a name="ado-security-design-features"></a>ADO 安全性設計功能
下列各節會說明安全性設計功能在 ActiveX Data Objects (ADO) 2.8 和更新版本。 在 ADO 2.8 已進行這些變更，以改善安全性。 ADO 6.0 中，包含在 Windows Vista 中的 Windows DAC 6.0 中，是功能上相當於 ADO 2.8，已包含在 Windows XP 和 Windows Server 2003 中的 MDAC 2.8。 本主題提供如何最能保護您的應用程式，在 ADO 中 2.8 或更新版本的相關資訊。

> [!IMPORTANT]
>  如果您要更新您的應用程式從 ADO 的較早版本，建議您測試更新的應用程式的非實際執行電腦，再將它部署給客戶。 如此一來，您可以確保在部署更新的應用程式之前，您已注意任何相容性問題。

## <a name="internet-explorer-file-access-scenarios"></a>Internet Explorer 檔案存取案例
 下列功能效果中使用時，ADO 2.8 和更新版本的運作方式編寫指令碼在 Internet Explorer 的網頁。

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>修訂和改進的安全性警告訊息方塊現在可用於警示的使用者
 ADO 2.7 和更早版本中，針對執行來自不受信任的提供者的 ADO 程式碼嘗試執行指令碼的網頁時，會出現下列警告訊息：

```console
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 ADO 2.8 和更新版本，如先前的訊息不會再出現。 相反地，在此內容中出現下列訊息：

```console
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 先前的訊息可讓使用者做出明智的決策，同時又知道或選擇的結果：

-   如果使用者信任的網站，按一下 [確定] 可讓所有的磁碟安全程式碼 （所有的 ADO 方法和屬性例外，本主題稍後所述的磁碟存取 Api） 來執行，並在瀏覽器視窗中執行。

-   如果使用者不信任的網站，按一下 取消封鎖來自執行，並在整個執行的資料存取的 ADO 程式碼。

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>磁碟存取現在僅限於受信任的站台的程式碼
 在 ADO 中明確限制一組有限的 Api，可能會公開可能會讀取或寫入至本機電腦上檔案的能力的 2.8 進行額外的設計變更。 以下是 API 方法已進一步執行 Internet Explorer 時，基於安全性考量限制：

-   Ado **Stream**物件，如果[LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md)或是[SaveToFile](../../ado/reference/ado-api/savetofile-method.md)使用的方法。

-   Ado**資料錄集**物件，如果有任一[儲存](../../ado/reference/ado-api/save-method.md)方法或[開啟](../../ado/reference/ado-api/open-method-ado-recordset.md)方法，例如當其中一個**adCmdFile**選項設定或[Microsoft OLE DB 持續性提供者 (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)用。

 這些有限的潛在磁碟存取的函式，如下列的行為便會發生 ADO 2.8 和更新版本，如果在 Internet Explorer 中執行任何會使用這些方法的程式碼：

-   如果提供的程式碼的站台之前已新增到信任的網站區域清單，在瀏覽器中執行的程式碼，並存取會授與本機檔案。

-   如果網站不會出現在 [信任的網站區域] 清單中，程式碼會封鎖，並拒絕存取本機檔案。

    > [!NOTE]
    >  在 ADO 2.8 和更新版本中，使用者未收到警示或建議將網站新增到信任的網站區域清單。 因此信任的網站清單的管理是人要部署或支援的網站為基礎的應用程式需要存取本機檔案系統的責任。

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>ActiveCommand 屬性在資料錄集物件上封鎖存取
 Internet Explorer 中執行時，ADO 2.8 現在會封鎖存取[ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md)屬性作用**資料錄集**物件，並傳回錯誤。 不論頁面是否來自信任的網站清單中註冊的網站，就會發生錯誤。

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>在處理中的 OLE DB 提供者和整合式的安全性的變更
 在檢閱 ADO 2.7 和更早的版本，針對潛在的安全性問題和考量，已發現下列案例：

 在某些情況下，OLE DB 提供者支援整合式安全性[DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx)屬性可能可能會允許執行指令碼的網頁以重複使用 ADO 連接物件，不小心連接到其他伺服器使用目前登入認證的使用者。 若要避免這個問題，ADO 2.8 和更新版本會處理取決於所選擇的方式提供，或未提供，針對整合式安全性的 OLE DB 提供者。

 從信任的網站區域的清單中列出的站台載入的網頁下, 表提供 ADO 2.8 和更新版本的每個案例中的 ADO 連接的管理方式的細目。

|使用者驗證，如 IE 設定登入|提供者會支援 「 整合式安全性 」 及 UID 和 PWD 被指定 (SQLOLEDB)|提供者不支援 「 整合式安全性 」 的 (JOLT，MSDASQL，MSPersist)|提供者支援 「 整合式安全性 」 並且將它設為 SSPI （指定沒有 UID PWD）|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|目前的使用者名稱和密碼的自動登入|允許連線|允許連線|允許連線|
|提示輸入使用者名稱和密碼|允許連線|連接失敗|連接失敗|
|只在近端內部網路區域自動登入|允許連線|提示使用者使用安全性警告|提示使用者使用安全性警告|
|匿名登入|允許連線|連接失敗|連接失敗|

 在案例中，安全性警告現在會出現，訊息方塊會通知使用者：

```console
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 先前的訊息可讓使用者做出更明智的決策，並視情況繼續執行。

> [!NOTE]
>  不受信任的網站 （也就是網站信任的網站區域清單中未列出），使用者如果提供者也不受信任 （如稍早在本章節中所述），可能會看到的資料列 」、 「 不安全的提供者的相關警告和 「 第二個警告的兩個安全性警告嘗試使用其身分識別。 如果使用者按一下 [確定] 的第一個警告，就會執行在上表中所述的回應行為程式碼與 Internet Explorer 設定。

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>控制 ADO 連接字串中是否傳回密碼文字
 當您嘗試取得的值[ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md) ADO 屬性**連線**物件時，會發生下列事件：

1.  如果連接已開啟，初始化呼叫會再進行基礎 OLE DB 提供者，以取得連接字串。

2.  根據設定中的 OLE DB 提供者[DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx)屬性，密碼是包含傳回的其他連接字串資訊。

 例如，如果 ADO 連接的動態屬性**Persist Security Info**設為 **，則為 True**，密碼資訊會包含在傳回的連接字串。 否則，如果基礎提供者已將屬性設定為**False** （例如使用 SQLOLEDB 提供者），傳回的連接字串中省略密碼資訊。

 如果您使用第三方 (亦即，非 Microsoft) 與 ADO 應用程式程式碼的 OLE DB 提供者，您可以檢查如何**DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO**屬性實作來判斷是否包含允許使用 ADO 連接字串的密碼資訊。

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>檢查非檔案裝置，當載入和儲存資料錄集或資料流
 ADO 2.7 和更早版本，如檔案輸入/輸出作業這類[開放](../../ado/reference/ado-api/open-method-ado-recordset.md)並[儲存](../../ado/reference/ado-api/save-method.md)用來讀取和寫入檔案為基礎的資料可能在某些情況下會允許的 URL 或檔案名稱來指定非磁碟基礎檔案類型。 例如，LPT1、 COM2、 PRN。TXT、 AUX 可做為別名用於印表機與輔助裝置之間系統使用特定的輸入/輸出

 已更新的 ADO 2.8 和更新版本中，這項功能。 開啟並儲存**Recordset**並**Stream**物件時，ADO 立即執行檔案型別檢查，以確認 URL 或檔案名稱中指定的輸入或輸出裝置的實際檔案。

> [!NOTE]
>  檔案類型檢查這一節所述僅適用於 Windows 2000 和更新版本。 它不適用於在較早的 Windows 版本，例如 Windows 98 ADO 2.8 或更新版本執行的情況。
