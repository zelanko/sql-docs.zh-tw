---
title: MSSQLSERVER_-1 | Microsoft Docs
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
f1_keywords:
- "-1"
helpviewer_keywords:
- -1 (Database Engine error)
ms.assetid: bad25b91-eaed-46c0-a5b7-71117a32304c
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: db2b101824c955bc4d691ad48f74a7dedb09cd47
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver-1"></a>MSSQLSERVER_-1
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|-1|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|建立伺服器的連接時發生錯誤。  連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，可能因為在預設的設定下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許遠端連接而引起此失敗  (提供者: SQL 網路介面，錯誤: 28 - 伺服器不支援要求的通訊協定) (Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，錯誤: -1)|  
  
## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端無法連接到伺服器。 此錯誤可能是由下列其中一項原因所造成：  
  
-   指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱無效。  
  
-   未啟用 TCP 或具名管道通訊協定。  
  
-   伺服器上的防火牆拒絕連接。  
  
-   未啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務 (sqlbrowser)。  
  
## <a name="user-action"></a>使用者動作  
若要解決這個錯誤，請嘗試下列任一動作：  
  
-   檢查在連接字串中指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱的拼字。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員工具，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接受透過 TCP 或具名管道通訊協定的遠端連接。 如需如何接受遠端連接的詳細資訊，請參閱[啟用或停用伺服器網路通訊協定](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。  
  
-   確認您已經將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器執行個體上的防火牆設為開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的通訊埠以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 通訊埠 (UDP 1434)。  
  
-   確認 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務已在伺服器上啟動。  
  
## <a name="see-also"></a>另請參閱  
[設定用於 Database Engine 存取的 Windows 防火牆](~/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
[設定用戶端通訊協定](~/database-engine/configure-windows/configure-client-protocols.md)  
[網路通訊協定和網路程式庫](~/sql-server/install/network-protocols-and-network-libraries.md)  
[用戶端網路組態](~/database-engine/configure-windows/client-network-configuration.md)  
[設定用戶端通訊協定](~/database-engine/configure-windows/configure-client-protocols.md)  
[啟用或停用伺服器網路通訊協定](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
