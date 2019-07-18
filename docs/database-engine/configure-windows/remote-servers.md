---
title: 遠端伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- server management [SQL Server], remote servers
- remote servers [SQL Server], configuring
- remote servers [SQL Server]
- servers [SQL Server], remote
- remote access option
ms.assetid: abf0fa24-f199-4273-9a1a-e8787ac9bee1
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 62af44faa45892be9af08a4fbd282ddfa4c7c757
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66772111"
---
# <a name="remote-servers"></a>遠端伺服器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  基於回溯相容性，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中支援遠端伺服器。 新應用程式應該改用連結的伺服器。 如需詳細資訊，請參閱 [連結的伺服器 &#40;Database Engine&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)。  
  
 遠端伺服器設定可讓連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的用戶端不須建立另一個連接，就可以在另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上執行預存程序。 而且，與用戶端連接的伺服器會接受用戶端的要求，並以用戶端的身分將要求傳送至遠端伺服器。 遠端伺服器會處理要求並將任何結果傳回到原始伺服器。 此伺服器接著就會將結果傳遞至用戶端。 設定遠端伺服器組態時，您應該也要考慮如何建立安全性。  
  
 如果您想要設定伺服器組態來執行另一個伺服器上的預存程序，但是並沒有現有的遠端伺服器組態時，請使用連結的伺服器來代替遠端伺服器。 對於連結的伺服器，您可以執行預存程序與分散式查詢；但是對於遠端伺服器，您只能執行預存程序。  
  
## <a name="remote-server-details"></a>遠端伺服器詳細資料  
 遠端伺服器是以配對設定。 若要設定遠端伺服器的配對，請將兩個伺服器都設定成可以相互辨識另一個為遠端伺服器。  
  
 大部份的情況下，您不需要設定遠端伺服器的組態選項。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在本機和遠端電腦上設定預設值，以允許遠端伺服器的連接。  
  
 若要讓遠端伺服器存取可以進行，在本機與遠端電腦上的 [遠端存取]  組態選項都必須設定為 1 (這是預設值)。[遠端存取]  會控制遠端伺服器的登入。 您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] **sp_configure** 預存程序或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]重設此組態選項。 若要重設 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的選項，請使用 [伺服器屬性連接]  頁面的 [允許此伺服器的遠端連接]  。 若要存取 [伺服器屬性連接]  頁面，請在物件總管中以滑鼠右鍵按一下伺服器名稱，然後按一下 [屬性]  。 在 [伺服器屬性]  頁面上，按一下 [連接]  頁面。  
  
 您可以從本機伺服器來停用遠端伺服器組態，以防止其配對遠端伺服器上的使用者存取本機伺服器。  
  
## <a name="security-for-remote-servers"></a>遠端伺服器的安全性  
 若要對遠端伺服器啟用遠端程序呼叫 (RPC)，您必須在遠端伺服器上，甚至在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的本機伺服器上，設定登入對應。 依預設，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中會停用 RPC。 此組態以減少其可攻擊介面區來加強伺服器的安全性。 在使用 RPC 之前，您必須先啟用此功能。 如需詳細資訊，請參閱 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
### <a name="setting-up-the-remote-server"></a>設定遠端伺服器  
 必須在遠端伺服器上設定遠端登入對應。 使用這些對應，遠端伺服器便可將來自指定伺服器之 RPC 連接的內送登入對應到本機登入。 遠端登入對應可使用 **sp_addremotelogin** 預存程序在遠端伺服器上進行設定。  
  
> [!NOTE]  
>  **不支援** sp_remoteoption  **的** trusted [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]選項。  
  
### <a name="setting-up-the-local-server"></a>設定本機伺服器  
 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證本機登入，您不需要在本機伺服器上設定登入對應。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用本機登入和密碼來連接至遠端伺服器。 若為 Windows 驗證登入，請在本機伺服器上設定本機登入對應，以定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體在建立遠端伺服器之 RPC 連接時所使用的登入與密碼。  
  
 若為 Windows 驗證所建立的登入，則您必須使用 **sp_addlinkedservlogin** 預存程序，來建立登入名稱與密碼的對應。 這個登入名稱與密碼必須與遠端伺服器所預期的內送登入和密碼相符，如同 **sp_addremotelogin**所建立的一樣。  
  
> [!NOTE]  
>  盡可能使用 Windows 驗證。  
  
### <a name="remote-server-security-example"></a>遠端伺服器安全性的範例  
 請考量這些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝： **serverSend** 和 **serverReceive**。 **serverReceive** 的設定是將來自 **serverSend** 的內送登入 (稱為 **Sales_Mary**) 對應到 **serverReceive** 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入 (稱為 **Alice**)。 另一個來自 **serverSend** 的內送登入 (稱為 **Joe**)，則會對應到 **serverReceive** 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入 (稱為 **Joe**)  。  
  
 下列的 Transact-SQL 程式碼範例會將 `serverSend` 設定為對 `serverReceive` 執行 RPC。  
  
```  
--Create remote server entry for RPCs   
--from serverSend in serverReceive.  
EXEC sp_addserver 'serverSend';  
GO  
  
--Create remote login mapping for login 'Sales_Mary' from serverSend  
--to Alice.  
EXEC sp_addremotelogin 'serverSend', 'Alice', 'Sales_Mary';  
GO  
--Create remote login mapping for login Joe from serverReceive   
--to same login.  
--Assumes same password for Joe in both servers.  
EXEC sp_addremotelogin 'serverSend', 'Joe', 'Joe';  
GO  
```  
  
 在 `serverSend`上，會針對 Windows 驗證登入 `Sales\Mary` 對應於登入 `Sales_Mary`來建立本機登入對應。 `Joe`不需本機對應，因為預設會使用相同的登入名稱與密碼，且 `serverReceive` 會具有 `Joe`的對應。  
  
```  
--Create a remote server entry for RPCs from serverReceive.  
EXEC sp_addserver 'serverReceive';  
GO  
--Create a local login mapping for the Windows authenticated login.  
--Sales\Mary to Sales_Mary. The password should match the  
--password for the login Sales_Mary in serverReceive.  
EXEC sp_addlinkedsrvlogin 'serverReceive', false, 'Sales\Mary',  
   'Sales_Mary', '430[fj%dk';  
GO  
```  
  
## <a name="viewing-local-or-remote-server-properties"></a>檢視本機或遠端伺服器屬性  
 您可以使用 **xp_msver** 擴充預存程序，來檢閱本機或遠端伺服器的伺服器屬性。 這些屬性包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的版本號碼、電腦的處理器類型和數目以及作業系統版本。 您可以從本機伺服器來檢視遠端伺服器的資料庫、檔案、登入與工具。 如需詳細資訊，請參閱 [xp_msver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-msver-transact-sql.md)。  
  
## <a name="related-tasks"></a>相關工作  
 [連結的伺服器 &#40;Database Engine&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)  
  
## <a name="related-content"></a>相關內容  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 [設定 remote access 伺服器組態選項](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)  
  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
