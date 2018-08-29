---
title: 建立新的已註冊伺服器 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.registerserver.general.sqlce.f1
- sql13.swb.registerserver.general.sqlserver.f1
helpviewer_keywords:
- Registered Servers [SQL Server], creating new registered servers
ms.assetid: 716ea070-a3b5-4514-9de2-82ce8a96514b
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c1d2c0f80d80a48005821038b2cb90367fef6cdd
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "42776225"
---
# <a name="create-a-new-registered-server-sql-server-management-studio"></a>建立新的已註冊伺服器 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  本主題描述如何藉由在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的「已註冊的伺服器」元件中註冊伺服器，來儲存您經常存取之伺服器的連接資訊。 您可以在連接之前或在連接時從 [物件總管] 註冊伺服器。 有一個特定的功能表選項，可用來註冊本機電腦上的伺服器執行個體。  
  
 已註冊的伺服器有兩種：  
  
-   本機伺服器群組  
  
     使用本機伺服器群組可輕鬆地連接您經常管理的伺服器。 本機伺服器和非本機伺服器都會在本機伺服器群組中註冊。 本機伺服器群組對於每一位使用者而言都是唯一的。 如需如何共用已註冊之伺服器的相關資訊，請參閱 [匯出已註冊的伺服器資訊 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/export-registered-server-information-sql-server-management-studio.md) 和 [匯入已註冊的伺服器資訊 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md)的「已註冊的伺服器」元件中註冊伺服器，來儲存您經常存取之伺服器的連接資訊。  
  
    > [!NOTE]  
    >  我們建議您盡可能使用 Windows 驗證。  
  
-   中央管理伺服器  
  
     中央管理伺服器會將伺服器組態儲存在中央管理伺服器中，而不是檔案系統上。 中央管理伺服器和從屬的已註冊伺服器只能使用 Windows 驗證來註冊。 在註冊中央管理伺服器之後，其關聯的已註冊伺服器將會自動顯示。 如需中央管理伺服器的詳細資訊，請參閱 [使用中央管理伺服器管理多部伺服器](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本無法指定為中央管理伺服器。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-automatically-register-the-local-server-instances"></a>自動註冊本機伺服器執行個體  
  
-   在 [已註冊的伺服器] 中，以滑鼠右鍵按一下 [已註冊的伺服器] 樹狀目錄的任何節點，然後按一下 [更新本機伺服器註冊]。  
  
#### <a name="to-create-a-new-registered-server"></a>建立新的已註冊伺服器  
  
1.  如果在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中看不到「已註冊的伺服器」，請在 **[檢視]** 功能表上按一下 **[已註冊的伺服器]**。  
  
     **伺服器類型**  
     從 [已註冊的伺服器] 註冊伺服器時，[伺服器類型] 方塊是唯讀的，且會與 [已註冊的伺服器] 窗格中所顯示的伺服器類型相符。 若要註冊不同類型的伺服器，請在 **[已註冊的伺服器]** 工具列上按一下 **[Database Engine]**、 **[Analysis Server]**、 **[Reporting Services]** 或 **[Integration Services]** ，然後再開始註冊新的伺服器。  
  
     **伺服器名稱**  
     選取要以下列格式註冊的伺服器執行個體：\<伺服器名稱>[\\\<執行個體名稱>]。  
  
     **驗證**  
     當連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體時，有兩種可用的驗證模式。  
  
     **Windows 驗證**  
     Windows 驗證模式允許使用者透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者帳戶連接。  
  
     **SQL Server 驗證**  
     當使用者從非信任連接使用指定的登入名稱與密碼進行連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會查看是否已設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入帳戶，以及指定的密碼是否符合先前記錄的密碼，自行執行驗證。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 沒有登入帳戶集，驗證將失敗，而使用者會收到錯誤訊息。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)] 如需詳細資訊，請參閱 [選擇驗證模式](../../relational-databases/security/choose-an-authentication-mode.md)。  
  
     **User name**  
     顯示您所連接的目前使用者名稱。 只有在您已選取使用 Windows 驗證進行連接時，才能使用此唯讀選項。 若要變更 **[使用者名稱]**，請以不同使用者登入電腦。  
  
     **登入**  
     輸入要用來連接的登入。 只有在您已選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接時，才可以使用此選項。  
  
     **密碼**  
     輸入登入的密碼。 只有在您已選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接時，才可以編輯此選項。  
  
     **記住密碼**  
     選取即可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 加密和儲存您輸入的密碼。 只有在您已選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接時，才會顯示此選項。  
  
    > [!NOTE]  
    >  如果您已儲存密碼而要停止儲存密碼，請清除此核取方塊，然後按一下 [儲存]。  
  
     **已註冊的伺服器名稱**  
     您要在 [已註冊的伺服器] 上顯示的名稱。 此名稱不需要與 **[伺服器名稱]** 方塊中的名稱相符。  
  
     **已註冊的伺服器描述**  
     輸入伺服器的選擇性描述。  
  
     **測試**  
     按一下以測試與 [伺服器名稱] 中選取之伺服器的連接。  
  
     **儲存**  
     按一下即可儲存已註冊的伺服器設定。  
  
## <a name="multiserver-queries"></a>多伺服器查詢  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [查詢編輯器] 視窗可以同時連接及查詢多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 此查詢傳回的結果可以合併到單一結果窗格，或者可以在不同的結果窗格中傳回。 還有一個選擇如下：[查詢編輯器] 所包含的資料行可提供產生每一個資料列的伺服器名稱，以及連接到提供每一個資料列之伺服器所用的登入。 如需如何執行多伺服器查詢的詳細資訊，請參閱[同時對多部伺服器執行陳述式 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/execute-statements-against-multiple-servers-simultaneously.md)。  
  
 若要針對本機伺服器群組內的所有伺服器執行查詢，請以滑鼠右鍵按一下伺服器群組，並指向 [連接]，然後按一下 [新增查詢]。 在新的 [查詢編輯器] 視窗中執行查詢時，將會使用包含使用者驗證內容的預存連接資訊，針對此群組中的所有伺服器來執行。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證所註冊但是未儲存密碼的伺服器將會連接失敗。  
  
 若要針對使用中央管理伺服器註冊的所有伺服器執行查詢，請展開中央管理伺服器，然後以滑鼠右鍵按一下伺服器群組，並指向 [連接]，再按一下 [新增查詢]。 在新的 [查詢編輯器] 視窗中執行查詢時，將會使用預存連接資訊及使用者的 Windows 驗證內容，針對此伺服器群組中的所有伺服器來執行。  
  
## <a name="see-also"></a>另請參閱  
 [在物件總管中隱藏系統物件](../object/hide-system-objects-in-object-explorer.md)   
 [匯出已註冊的伺服器資訊 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/export-registered-server-information-sql-server-management-studio.md)   
 [匯入已註冊的伺服器資訊 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md)  
  
  
