---
title: 通用資料連結（UDL）設定 |Microsoft Docs
description: 使用適用于 SQL Server 的 Microsoft OLE DB 驅動程式進行通用資料連結（UDL）設定
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: d92555fba1d9e0a380ffdc9051817ddfae9ca4b7
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381763"
---
# <a name="universal-data-link-udl-configuration"></a>通用資料連結 (UDL) 設定
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>連線索引標籤
使用 [連接] 索引標籤，指定如何使用適用于 SQL Server 的 Microsoft OLE DB 驅動程式來連接到您的資料。

![OLE DB 資料連結頁面的螢幕擷取畫面-[連接] 索引標籤](../media/data-link-pages-connection-tab.png)

[連線] 索引標籤是提供者特有的，而且只會顯示 Microsoft OLE DB Driver for SQL Server 所需的連線屬性。

|選項|Description|
|---   |---        |
|選取或輸入伺服器名稱|從下拉式清單中選取伺服器名稱，或是輸入您要存取之資料庫所在的伺服器位置。 在伺服器上選取資料庫是個別的動作。 按一下 [重新整理]，以更新此清單。
|輸入要登入伺服器的資訊|您可以從這個下拉式清單中選取下列驗證選項： <ul><li>使用目前登入之使用者的 Windows 帳號憑證，`Windows Authentication:` 驗證 SQL Server。</li><li>使用登入識別碼和密碼 `SQL Server Authentication:` 驗證。</li><li>使用 Azure Active Directory 身分識別 `Active Directory - Integrated:` 整合式驗證。 此模式也可用於 Windows 驗證以 SQL Server。</li><li>`Active Directory - Password:` 具有 Azure Active Directory 身分識別的使用者識別碼和密碼驗證。</li><li>`Active Directory - Universal with MFA support:` 具有 Azure Active Directory 身分識別的互動式驗證。 此模式支援 Azure 多重要素驗證（MFA）。</li></ul>|
|伺服器 SPN|如果您使用了信任連接，就可以指定伺服器的服務主要名稱 (SPN)。|
|[使用者名稱]|輸入當您登入資料來源時要用來進行驗證的使用者識別碼。|
|[密碼]|輸入當您登入資料來源時要用來進行驗證的密碼。|
|空白密碼|核取時，可讓指定的提供者在連接字串中使用空白密碼。|
|允許儲存密碼|核取時，允許將密碼與連接字串一起儲存。 密碼是否可包含於連接字串中完全取決於呼叫應用程式的功能。 <br/><br/>**注意：** 若已儲存，系統會傳回密碼並以未遮罩與未加密的方式儲存密碼。|
|使用高度加密資料|若有選取時，透過連接傳遞的資料將會加密。|
|信任伺服器憑證|若有選取時，將會驗證服務器的憑證。 伺服器的憑證必須具有伺服器的正確主機名稱，並由受信任的憑證授權單位單位發行。|
|選取資料庫|選取或輸入您想要存取的資料庫名稱。|
|附加資料庫檔案做為資料庫名稱|為可附加的資料庫指定主要檔案的名稱。 此資料庫會附加並且當做資料來源的預設資料庫使用。 在此區段下的第一個文字方塊中，輸入要用於附加資料庫檔案的資料庫名稱。<br/><br/>在標示為 [`Using the filename`] 的文字方塊中輸入要附加之資料庫檔案的完整路徑，或按一下 [`...`] 按鈕以流覽資料庫檔案。|
|變更密碼|顯示 [變更 SQL Server 密碼] 對話方塊。 |
|[測試連接]|按一下以嘗試連接到指定的資料來源。 如果連接失敗，請確定設定正確無誤。 例如，拼字錯誤和區分大小寫都可能會導致連接失敗。|

## <a name="advanced-tab"></a>進階索引標籤
使用 [Advanced] 索引標籤可查看和設定其他初始化屬性。

![OLE DB 資料連結頁面的螢幕擷取畫面-[Advanced] 索引標籤](../media/data-link-pages-advanced-tab.png)

|選項|Description|
|---   |---        |
| 連接逾時 | 指定 Microsoft OLE DB 驅動程式 SQL Server 等候初始化完成的時間量（以秒為單位）。 如果初始化逾時，系統就會傳回錯誤而且不會建立連接。|


> [!NOTE]  
>  如需更一般的資料連結連接資訊，請參閱[資料連結 API 總覽](https://go.microsoft.com/fwlink/?linkid=2067432)。

## <a name="next-steps"></a>後續步驟
- 使用 OLE DB 驅動程式[向 Azure Active Directory 進行驗證](../features/using-azure-active-directory.md)。

- 使用 OLE DB 驅動程式[提示使用者輸入驗證認證](../help-topics/sql-server-login-dialog.md)。