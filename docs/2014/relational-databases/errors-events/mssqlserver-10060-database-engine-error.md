---
title: MSSQLSERVER_10060 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "10060"
helpviewer_keywords:
- 10060 (Database Engine error)
ms.assetid: 28c21277-cad8-406c-a955-07933a56982a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee37bfd2c2ba17377589f8a3e744cc018b9d5775
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119428"
---
# <a name="mssqlserver10060"></a>MSSQLSERVER_10060
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|10060|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|建立伺服器的連接時發生錯誤。  連接到 SQL Server 時，可能因為在預設的設定下 SQL Server 不允許遠端連接而引起此失敗。 (提供者: TCP 提供者，錯誤: 0 - 連線嘗試失敗，因為連線對象有一段時間並未正確回應，或是連線建立失敗，因為連線的主機無法回應。) (Microsoft SQL Server，錯誤: 10060)|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端無法連接到伺服器。 發生這個錯誤的原因，可能是伺服器上的防火牆拒絕連接，或伺服器未設定成接受遠端連接。  
  
## <a name="user-action"></a>使用者動作  
 若要解決這個錯誤，請嘗試下列任一動作：  
  
-   確定已將電腦上的防火牆設定成允許這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體接受連接。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員工具，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定成接受遠端連接。  
  
## <a name="see-also"></a>另請參閱  
 [設定用於 Database Engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [設定用戶端通訊協定](../../database-engine/configure-windows/configure-client-protocols.md)   
 [網路通訊協定和網路程式庫](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [用戶端網路組態](../../database-engine/configure-windows/client-network-configuration.md)   
 [設定用戶端通訊協定](../../database-engine/configure-windows/configure-client-protocols.md)   
 [啟用或停用伺服器網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
