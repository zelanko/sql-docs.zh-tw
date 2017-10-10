---
title: "SQL Server 登入對話方塊 (ODBC) |Microsoft 文件"
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 67aa8fc08a75efbcf77eb839b1999961a17e2a9f
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="sql-server-login-dialog-box-odbc"></a>SQL Server 登入對話方塊 (ODBC)

當您呼叫 ODBC 連接沒有指定足夠的資訊來連接到 SQL Server，則 ODBC 驅動程式會顯示驅動程式**SQL Server 登入** 對話方塊。

## <a name="options"></a>選項。

### <a name="server"></a>Server

您的網路上的 SQL Server 執行個體名稱。 從清單中，選取伺服器 \ 執行個體名稱，或輸入中的伺服器 \ 執行個體名稱**伺服器**方塊。 （選擇性） 您可以建立伺服器別名，用戶端電腦使用**SQL Server 組態管理員**，然後輸入該名稱在**伺服器**方塊。

當您使用相同的電腦與 SQL Server，您可以輸入"(local)"。 您可以連接到 SQL Server，即使當執行是非網路版的 SQL Server 本機執行個體。

如需有關不同網路類型的伺服器名稱的詳細資訊，請參閱 SQL Server 線上叢書 》 中的 SQL Server 安裝文件。

### <a name="authentication-mode"></a>驗證模式

從下列其中一種選取驗證模式：
- **SQL Server**登入識別碼和密碼
- **Windows 整合式**使用目前登入的使用者帳戶進行驗證
- **Active Directory 密碼**登入識別碼和密碼
- **Active Directory Integrated**使用目前登入的使用者帳戶進行驗證

請參閱[資料來源精靈螢幕 2](../../../connect/odbc/windows/dsn-wizard-2.md)如需有關驗證模式。

### <a name="server-spn"></a>伺服器 SPN

如果您使用了信任連接，就可以指定伺服器的服務主要名稱 (SPN)。

### <a name="login-id"></a>登入識別碼

指定要用於連接，如果 SQL Server 或 Azure Active Directory 登入識別碼**驗證模式**設**SQL Server**或**Active Directory 密碼**。 否則，**登入識別碼**方塊已停用。

### <a name="password"></a>密碼

指定的密碼。 如果用於連接的 SQL Server 或 Azure Active Directory 登入識別碼**驗證模式**設**SQL Server**或**Active Directory 密碼**. 否則，**密碼**方塊已停用。

### <a name="options"></a>選項。

顯示或隱藏**選項**群組。 **選項**按鈕已啟用，如果**伺服器**的值。

### <a name="change-password"></a>變更密碼

選取此方塊時，會顯示**新密碼**和**確認新密碼**方塊。

### <a name="new-password"></a>新密碼

指定新的密碼。

### <a name="confirm-new-password"></a>確認新密碼

再次指定新密碼，以進行確認。

### <a name="database"></a>資料庫

指定用於連接的預設資料庫。 此設定會覆寫伺服器上指定用於登入的預設資料庫。 如果未指定任何資料庫，則連接會使用伺服器上指定用於登入的預設資料庫。

### <a name="mirror-server"></a>鏡像伺服器

指定要鏡像處理之資料庫的容錯移轉夥伴名稱。

### <a name="mirror-spn"></a>鏡像 SPN

(選擇性) 您可以指定鏡像伺服器的 SPN。 鏡像伺服器的 SPN 會用於用戶端與伺服器之間的相互驗證。

### <a name="language"></a>語言

指定要用於 SQL Server 系統訊息的國家語言。 執行 SQL Server 的電腦必須安裝的語言。 此設定會覆寫伺服器上指定用於登入的預設語言。 如果未指定任何語言，則連接會使用伺服器上指定用於登入的預設語言。

### <a name="application-name"></a>Application Name

（選擇性）指定要儲存在應用程式名稱**sys.sysprocesses**此連接的資料列中的資料行**sys.sysprocesses**。

### <a name="workstation-id"></a>工作站 ID

（選擇性）指定要儲存在中的工作站識別碼**hostname**此連接的資料列中的資料行**sys.sysprocesses**。

### <a name="use-strong-encryption-for-data"></a>使用高度加密資料

選取時，將會加密透過連線傳送的資料。 預設會加密登入，即使清除該核取方塊亦然。

### <a name="trust-server-certificate"></a>信任伺服器憑證

時，此選項時才適用**使用高度加密資料**已啟用。 選取時，伺服器的憑證會驗證伺服器的正確的主機名稱，然後再由受信任的憑證授權單位發出。

## <a name="see-also"></a>另請參閱

[Windows 上適用於 SQL Server 的 Microsoft ODBC 驅動程式](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)

