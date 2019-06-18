---
title: 通用資料連結 (UDL) 設定 |Microsoft Docs
description: 使用 Microsoft OLE DB Driver for SQL Server 的通用資料連結 (UDL) 設定
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: e198f561fd4f6bcec390ef8632c1cdc96f2810d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62854658"
---
# <a name="universal-data-link-udl-configuration"></a>通用資料連結 (UDL) 設定
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>連線索引標籤
您可以使用 [連線] 索引標籤來指定如何連接到您使用 Microsoft OLE DB Driver for SQL Server 的資料。

![OLE DB 資料連結頁面連線 索引標籤的螢幕擷取畫面](../media/data-link-pages-connection-tab.png)

[連線] 索引標籤是提供者特有的，而且只會顯示 Microsoft OLE DB Driver for SQL Server 所需的連線屬性。

|選項|Description|
|---   |---        |
|選取或輸入伺服器名稱|從下拉式清單中選取伺服器名稱，或是輸入您要存取之資料庫所在的伺服器位置。 在伺服器上選取資料庫是個別的動作。 按一下 [重新整理]，以更新此清單。
|輸入資訊以登入伺服器|您可以從這個下拉式清單選取下列的驗證選項： <ul><li>`Windows Authentication:` 使用目前登入使用者的 Windows 帳戶認證的 SQL Server 驗證。</li><li>`SQL Server Authentication:` 使用登入識別碼和密碼的 SQL Server 驗證。</li><li>`Active Directory - Integrated:` 使用目前登入使用者的 Windows 帳戶認證的整合式的驗證。</li><li>`Active Directory - Password:` 使用登入識別碼和密碼的 active Directory 驗證。</li></ul>|
|伺服器 SPN|如果您使用了信任連接，就可以指定伺服器的服務主要名稱 (SPN)。|
|[使用者名稱]|輸入要用於驗證，當您登入的資料來源的使用者識別碼。|
|[密碼]|輸入要用於驗證，當您登入的資料來源的密碼。|
|空白密碼|有選取時，可讓指定的提供者的連接字串中使用空白密碼。|
|允許儲存密碼|有選取時，可讓儲存的連接字串的密碼。 密碼是否可包含於連接字串中完全取決於呼叫應用程式的功能。 <br/><br/>**注意：** 若已儲存，系統會傳回密碼並以未遮罩與未加密的方式儲存密碼。|
|使用高度加密資料|有選取時，會透過連線傳遞的資料將會加密。|
|信任伺服器憑證|有選取時，將會驗證伺服器的憑證。 伺服器的憑證必須具有伺服器的正確主機名稱，且受信任的憑證授權單位所核發。|
|選取資料庫|選取或輸入您想要存取的資料庫名稱。|
|附加資料庫檔案做為資料庫名稱|為可附加的資料庫指定主要檔案的名稱。 此資料庫會附加並且當做資料來源的預設資料庫使用。 在此區段下第一個文字方塊中，輸入要用於附加的資料庫檔案的資料庫名稱。<br/><br/>輸入要在文字方塊中標示為可附加的資料庫檔案的完整路徑`Using the filename`，或按一下`...`按鈕以瀏覽資料庫檔案。|
|變更密碼|顯示變更 SQL Server 密碼 對話方塊。 |
|[測試連接]|按一下此選項，以嘗試連線到指定的資料來源。 如果連接失敗，請確定設定正確無誤。 例如，拼字錯誤和區分大小寫都可能會導致連接失敗。|

## <a name="advanced-tab"></a>進階索引標籤
您可以使用 [進階] 索引標籤來檢視和設定額外的初始化屬性。

![OLE DB 資料連結頁面-進階 索引標籤的螢幕擷取畫面](../media/data-link-pages-advanced-tab.png)

|選項|Description|
|---   |---        |
| 連接逾時 | 指定的 Microsoft OLE DB Driver for SQL Server 等候初始化完成的時間 （以秒為單位）。 如果初始化逾時，系統就會傳回錯誤而且不會建立連接。|


> [!NOTE]  
>  如需一般連結的資料連接資訊，請參閱[資料連結 API 概觀](https://go.microsoft.com/fwlink/?linkid=2067432)。

## <a name="next-steps"></a>後續步驟
- [向 Azure Active Directory](../features/using-azure-active-directory.md)使用 OLE DB 驅動程式。

- [提示使用者提供驗證認證](../help-topics/sql-server-login-dialog.md)使用 OLE DB 驅動程式。