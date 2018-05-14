---
title: MSSQLSERVER_21879 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 21879 (Database Engine error)
ms.assetid: fcfab735-05ca-423a-89f1-fdee7e2ed8c0
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7e802bb805de95370c51b3cbcb17f62ed367a27b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver21879"></a>MSSQLSERVER_21879
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|21879|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum21879|  
|訊息文字|無法查詢原始發行者 '%s' 和發行者資料庫 '%s' 的重新導向伺服器 '%s' 以判斷遠端伺服器之名稱; 錯誤 %d，錯誤訊息 '%s'。|  
  
## <a name="explanation"></a>說明  
**sp_validate_redirected_publisher** 會使用暫時連結的伺服器，而建立此伺服器的目的是要連接到重新導向的發行者，以便探索遠端伺服器的名稱。 當連結的伺服器查詢失敗時，就會傳回錯誤 21879。 要求遠端伺服器名稱的呼叫通常是在第一次使用暫時連結的伺服器時進行，因此如果發生連接問題，這些問題可能會先與此呼叫一起顯示。 這個遠端呼叫只會在遠端伺服器上執行選取的 **@@servername**。  
  
用來查詢重新導向發行者的連結伺服器，會使用針對原始發行者呼叫 **sp_adddistpublisher** 時所提供的安全性模式、登入和密碼。  
  
-   如果使用了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證 (安全性模式 0)，則指定的登入和密碼就會用來連接到遠端伺服器。  
  
-   如果使用了 Windows 驗證 (安全性模式 1)，就會使用信任的連接進行連接。  
  
    -   如果使用者明確呼叫了 **sp_validate_redirected_publisher**，就會使用其在 Windows 中所用的登入進行連接。  
  
    -   如果複寫代理程式從 **sp_get_redirected_publisher** 呼叫 **sp_validate_redirected_** publisher，就會使用與代理程式相關聯的 Windows 登入。  
  
錯誤 21879 可能表示呼叫 **sp_validate_redirected_publisher** 時使用了重新導向目標發行者未知的登入。  
  
## <a name="user-action"></a>使用者動作  
請確定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入或 Windows 驗證登入在所有可用性群組複本上有效，而且具有足夠的授權，可存取發行者資料庫中的訂閱中繼資料資料表 (syssubscriptions 和 sysmergesubscriptions)。  
  
如果複寫代理程式是在散發者以外的節點上執行 (例如在訂閱者端執行的合併代理程式)，當其起始的 **sp_get_redirected_publisher** 呼叫傳回錯誤 21879 時，就會存在一些特殊考量。 如果 Windows 驗證用於重新導向發行者的連接，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就必須設定為 Kerberos 驗證，才能成功建立連接。 當您使用 Windows 驗證而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並未設定為 Kerberos 驗證時，在訂閱者端執行的合併代理程式就會收到表示 'NT AUTHORITY\ANONYMOUS LOGON' 登入失敗的錯誤 18456。 可解決此問題的方式有三種：  
  
-   將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為 Kerberos 驗證。 請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書中的 **Kerberos 驗證和 SQL Server**。  
  
-   使用 **sp_changedistpublisher** 來變更與 MSdistpublishers 中之原始發行者相關聯的安全性模式，並且指定要用於連接的登入和密碼。  
  
-   在合併代理程式命令列上指定命令列參數 *BypassPublisherValidation*，以便在散發者端呼叫 **sp_get_redirected_publisher** 時略過驗證。  
  
