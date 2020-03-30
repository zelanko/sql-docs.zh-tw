---
title: SQL Server 登入對話方塊 (OLE DB) | Microsoft Docs
description: 使用 SQL Server 登入對話方塊
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: d35c339798b4385cb903d8a4a83f13184bbf4db3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "72381750"
---
# <a name="sql-server-login-dialog-box"></a>SQL Server 登入對話方塊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

當您嘗試連線但未指定足夠資訊時，OLE DB 驅動程式會顯示 [SQL Server 登入]  對話方塊。

> [!NOTE]  
> SQL Server 登入對話方塊的提示行為會由 `DBPROP_INIT_PROMPT` 初始化屬性所控制。 如需詳細資訊，請參閱
> - [初始化和授權屬性](../ole-db-data-source-objects/initialization-and-authorization-properties.md)
> - [OLE DB 程式設計人員指南](https://go.microsoft.com/fwlink/?linkid=2067702)

![[SQL Server 登入] 對話方塊的螢幕擷取畫面](../media/sql-server-login-dialog.png)

## <a name="options"></a>選項。
|選項|描述|
|---   |---        |
|伺服器|網路上 SQL Server 執行個體的名稱。 從清單中選取伺服器或執行個體名稱，或在 [伺服器]  方塊中鍵入伺服器或執行個體名稱。 (選擇性) 您可以在用戶端電腦上使用 [SQL Server 設定管理員]  建立伺服器別名，並在 [伺服器]  方塊中鍵入該名稱。 <br/><br/>如果您使用的電腦與 SQL Server 的相同，則可輸入 "(local)"。 接著，即使執行的是非網路版的 SQL Server，您也可連接到 SQL Server 的本機執行個體。<br/><br/>如需適用於不同網路類型之伺服器名稱的詳細資訊，請參閱 [SQL Server 安裝](https://go.microsoft.com/fwlink/?linkid=2067541)。|
|驗證模式|您可以從下拉式清單中選取下列驗證選項：<br/><ul><li>`Windows Authentication:`使用目前登入之使用者的 Windows 帳戶認證來向 SQL Server 進行的驗證。</li><li>`SQL Server Authentication:`使用登入識別碼和密碼進行的驗證。</li><li>`Active Directory - Integrated:`以 Azure Active Directory 識別進行的整合式驗證。 此模式也可以用於向 SQL Server 進行的 Windows 驗證。</li><li>`Active Directory - Password:`以 Azure Active Directory 識別進行的使用者識別碼和密碼驗證。</li><li>`Active Directory - Universal with MFA support:`以 Azure Active Directory 識別進行的互動式驗證。 此模式支援 Azure Multi-Factor Authentication (MFA)。</li></ul>|
|伺服器 SPN|如果您使用了信任連接，就可以指定伺服器的服務主要名稱 (SPN)。|
|登入識別碼|指定要針對連線使用的登入識別碼。 只有當 `Authentication Mode` 設定為 `SQL Server Authentication`、`Active Directory - Password` 或 `Active Directory - Universal with MFA support` 時，才會啟用 [登入識別碼] 文字方塊。|
|密碼|指定要針對連線使用的密碼。 只有當 `Authentication Mode` 設定為 `SQL Server Authentication` 或 `Active Directory - Password` 時，才會啟用 [密碼] 文字方塊。|
|選項。|顯示或隱藏 [選項]  群組。 如果 [伺服器]  具有值，即會啟用 [選項]  按鈕。|
|變更密碼|核取時，會啟用 [新密碼]  和 [確認新密碼]  文字方塊。|
|新密碼|指定新的密碼。|
|確認新密碼|再次指定新密碼，以進行確認。|
|資料庫|選取或輸入用於連線的預設資料庫。 此設定會覆寫伺服器上指定用於登入的預設資料庫。 如果未指定任何資料庫，則連接會使用伺服器上指定用於登入的預設資料庫。|
|鏡像伺服器|指定要鏡像處理之資料庫的容錯移轉夥伴名稱。|
|鏡像 SPN|(選擇性) 您可以指定鏡像伺服器的 SPN。 鏡像伺服器的 SPN 會用於用戶端與伺服器之間的相互驗證。|
|Language|指定要用於 SQL Server 系統訊息的國家/地區語言。 執行 SQL Server 的電腦必須安裝此語言。 此設定會覆寫伺服器上指定用於登入的預設語言。 如果未指定任何語言，則連接會使用伺服器上指定用於登入的預設語言。|
|應用程式名稱|指定要針對 **sys.sysprocesses** 中的此連線，儲存在資料列上的 **program_name** 資料行中的應用程式名稱。|
|工作站 ID|指定要針對 **sys.sysprocesses** 中的此連線，儲存在資料列上的 **hostname** 資料行中的工作站識別碼。|
|使用高度加密資料|核取時，透過連線傳遞的資料將會加密。|
|信任伺服器憑證|核取時，將會驗證伺服器的憑證。 伺服器的憑證必須具有伺服器的正確主機名稱，且由信任的憑證授權單位所發出。|

> [!NOTE]  
> 使用 `Windows Authentication` 或 `SQL Server Authentication` 模式時，只有在啟用 [為資料使用增強式加密]  選項時，才會考慮使用**信任伺服器憑證**。

## <a name="next-steps"></a>後續步驟
- 使用 OLE DB 驅動程式[向 Azure Active Directory 進行驗證](../features/using-azure-active-directory.md)。
- 使用[通用資料連結 (UDL)](data-link-pages.md) 設定連線資訊。