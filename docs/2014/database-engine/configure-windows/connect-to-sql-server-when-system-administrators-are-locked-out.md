---
title: 當系統管理員遭鎖定在外時連線到 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- sa account
- connecting when locked out [SQL Server]
- locked out [SQL Server]
ms.assetid: c0c0082e-b867-480f-a54b-79f2a94ceb67
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e4a6f1d769833a451f7360c747249cb28d0d0c12
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022697"
---
# <a name="connect-to-sql-server-when-system-administrators-are-locked-out"></a>當系統管理員遭到鎖定時連接到 SQL Server
  本主題描述如何以系統管理員的身分，重新取得 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的存取權。 系統管理員可能因為下列其中一個原因而失去 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的存取權：  
  
-   屬於 sysadmin 固定伺服器角色之成員的所有登入都因為錯誤而遭到移除。  
  
-   屬於 sysadmin 固定伺服器角色之成員的所有 Windows 群組都因為錯誤而遭到移除。  
  
-   屬於 sysadmin 固定伺服器角色之成員的登入供已經離開公司或沒有空的個人使用。  
  
-   sa 帳戶已遭到停用或沒有人知道密碼。  
  
 您可以重新取得存取權的其中一種方式就是重新安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並將所有資料庫附加到新的執行個體。 這個解決方案相當耗時，而且，若要復原登入，可能需要從備份還原 master 資料庫。 如果 master 資料庫的備份較舊，可能不會有所有的資訊。 如果 master 資料庫的備份比較新，可能與先前的執行個體擁有相同的登入，因此，系統管理員仍然會遭到鎖定。  
  
## <a name="resolution"></a>解決方案  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -m **或** -f **選項，在單一使用者模式中啟動** 的執行個體。 接著，電腦本機管理員群組的任何成員都可以利用 sysadmin 固定伺服器角色的成員身分，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
> [!NOTE]  
>  當您以單一使用者模式啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，請先停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務。 否則， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 可能會先進行連接，您就無法以另一個使用者的身分進行連接。  
  
 當您搭配 **sqlcmd** 或 **使用** -m [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]選項時，您可以限制與指定之用戶端應用程式之間的連接。 例如， **-m"sqlcmd"** 會將連接限制為單一連接，而且該連接必須具有 **sqlcmd** 用戶端程式的識別。 當您在單一使用者模式下啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而且有未知的用戶端應用程式佔用唯一可用的連接時，請使用這個選項。 若要透過 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的查詢編輯器進行連接，請使用 **-m"Microsoft SQL Server Management Studio - Query"**。  
  
> [!IMPORTANT]  
>  請勿將這個選項當做安全性功能使用。 用戶端應用程式會提供用戶端應用程式名稱，而且可能會在連接字串中提供假的名稱。  
  
 如需如何以單一使用者模式啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的逐步指示，請參閱[設定伺服器啟動選項 &#40;SQL Server 組態管理員&#41;](scm-services-configure-server-startup-options.md)。  
  
## <a name="step-by-step-instructions"></a>逐步指示  
 下列指示描述連接到在 Windows 8 或更新版上執行之 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的程序。 針對舊版 SQL Server 或 Windows 提供了些微調整。 您必須在登入 Windows 成為本機 Administrators 群組的成員時執行這些指示，而且這些指示會假設電腦已安裝了 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
1.  在起始頁上，啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 在 [檢視] 功能表上，選取 [已註冊的伺服器] (如果您的伺服器尚未註冊，請以滑鼠右鍵按一下 [本機伺服器群組]，指向 [工作]，然後按一下 [註冊本機伺服器])。  
  
2.  在 [已註冊的伺服器] 區域中，以滑鼠右鍵按一下您的伺服器，然後按一下 [SQL Server 組態管理員]。 這樣應該會要求以系統管理員身分執行的權限，然後開啟組態管理員程式。  
  
3.  關閉 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。  
  
4.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員的左窗格中，選取 [SQL Server 服務]。 在右窗格中，尋找您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體  ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體會在電腦名稱後面加上 **(MSSQLSERVER)**。 具名執行個體會以 [已註冊的伺服器] 中顯示的相同大寫名稱出現)。以滑鼠右鍵按一下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，然後按一下 [屬性]。  
  
5.  在**啟動參數**索引標籤的**指定啟動參數**方塊中，輸入`-m`，然後按一下  `Add`。 (這是虛線，然後接著小寫字母 m)。  
  
    > [!NOTE]  
    >  如果是某些舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則沒有 [啟動參數] 索引標籤。在該情況下，請在 [進階] 索引標籤上，按兩下 [啟動參數]。 這些參數就會在非常小的視窗中開啟。 請小心不要變更任何現有參數。 在結尾，加入新的參數`;-m`，然後按一下  `OK`。 (這是分號，然後接著虛線和小寫字母 m)。  
  
6.  按一下`OK`，並在之後重新啟動的訊息，以滑鼠右鍵按一下您的伺服器名稱，然後按一下**重新啟動**。  
  
7.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後，您的伺服器即會處於單一使用者模式。 確定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 並未執行。 如果已啟動，它將會佔用您的唯一連接。  
  
8.  在 Windows 8 的 [開始] 畫面上，以滑鼠右鍵按一下 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的圖示。 在畫面底部，選取 [以系統管理員身分執行] (這樣會將您的系統管理員認證傳遞給 SSMS)。  
  
    > [!NOTE]  
    >  如果是舊版 Windows，[以系統管理員身分執行] 選項會顯示成子功能表。  
  
     在某些組態中，SSMS 會嘗試建立許多連接。 多重連接將會失敗，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處於單一使用者模式。 您可以選取下列其中一項動作來執行。 執行下列其中一項動作。  
  
    1.  使用 Windows 驗證 (包含您的系統管理員認證) 透過 [物件總管] 連接。 依序展開 [安全性] 和 [登入]，然後按兩下您自己的登入。 在**伺服器角色**頁面上，選取`sysadmin`，然後按一下  `OK`。  
  
    2.  不透過 [物件總管] 連接，而是使用 Windows 驗證 (包含您的系統管理員認證) 透過查詢視窗連接  (如果您沒有透過 [物件總管] 連接，就只能以這種方式連接)。執行程式碼如下所示，加入新的 Windows 驗證登入的成員`sysadmin`固定的伺服器角色。 下列範例會加入名為 `CONTOSO\PatK` 的網域使用者。  
  
        ```  
        CREATE LOGIN [CONTOSO\PatK] FROM WINDOWS;  
        ALTER SERVER ROLE sysadmin ADD MEMBER [CONTOSO\PatK];  
        ```  
  
    3.  如果您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是以混合驗證模式執行，請使用 Windows 驗證 (包含您的系統管理員認證) 透過查詢視窗連接。 執行程式碼如下所示，建立新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證登入的成員`sysadmin`固定的伺服器角色。  
  
        ```  
        CREATE LOGIN TempLogin WITH PASSWORD = '************';  
        ALTER SERVER ROLE sysadmin ADD MEMBER TempLogin;  
        ```  
  
        > [!WARNING]  
        >  請將 ************ 取代成增強式密碼。  
  
    4.  如果您[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]混合驗證模式中的執行，而且您想要重設密碼的`sa`帳戶時，透過使用 Windows 驗證 （包含您的系統管理員認證） 的查詢視窗連接。 變更密碼`sa`使用下列語法的帳戶。  
  
        ```  
        ALTER LOGIN sa WITH PASSWORD = '************';  
        ```  
  
        > [!WARNING]  
        >  請將 ************ 取代成增強式密碼。  
  
9. 下列步驟現在會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 變更回多使用者模式。 關閉 SSMS。  
  
10. 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員的左窗格中，選取 [SQL Server 服務]。 在右窗格中，以滑鼠右鍵按一下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，然後按一下 [屬性]。  
  
11. 在**啟動參數**索引標籤的**現有參數**方塊中，選取`-m`，然後按一下  `Remove`。  
  
    > [!NOTE]  
    >  如果是某些舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則沒有 [啟動參數] 索引標籤。在該情況下，請在 [進階] 索引標籤上，按兩下 [啟動參數]。 這些參數就會在非常小的視窗中開啟。 移除`;-m`您加入更早版本，然後再按一下其中`OK`。  
  
12. 以滑鼠右鍵按一下您的伺服器名稱，然後按一下 [重新啟動]。  
  
 現在您應該能夠正常連接與其中一個目前屬於成員帳戶的`sysadmin`固定的伺服器角色。  
  
## <a name="see-also"></a>另請參閱  
 [以單一使用者模式啟動 SQL Server](start-sql-server-in-single-user-mode.md)   
 [Database Engine 服務啟動選項](database-engine-service-startup-options.md)  
  
  