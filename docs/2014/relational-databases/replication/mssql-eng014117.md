---
title: MSSQL_ENG014117 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014117 error
ms.assetid: e5906a76-9511-4c47-8826-8c765b58a39d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec41205836a2e367d6fb270e532a505979a3e178
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52758180"
---
# <a name="mssqleng014117"></a>MSSQL_ENG014117
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|14117|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|'%s' 並未設定為散發資料庫。|  
  
## <a name="explanation"></a>說明  
 如果下列條件中的一或兩條成立，則會發生此錯誤：  
  
-   **msdb..MSdistributiondbs**中遺失指定散發資料庫的項目。  
  
-   **master** 資料庫中沒有本機伺服器的項目，或者該項目不正確。  
  
     針對拓撲中所有伺服器，複寫預計應使用電腦名稱與選擇性的執行個體名稱註冊 (叢集執行個體則為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 虛擬伺服器名稱加上選擇性的執行個體名稱)。 要讓複寫正常運作， `SELECT @@SERVERNAME` 針對拓撲中每部伺服器傳回的值，都應該符合電腦名稱或虛擬伺服器名稱加上選擇性執行個體名稱。  
  
     若您已透過 IP 位址或完整格式的網域名稱 (FQDN) 註冊任一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，就不支援複寫。 如果您設定複寫時，依 IP 位址或依 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 FQDN 註冊了任何 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 執行個體，就可能會引發這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
 請確認「散發者」執行個體註冊正確。 若電腦網路名稱和 SQL Server 執行個體名稱不符，則：  
  
-   加入 SQL Server 執行個體名稱做為有效網路名稱。 設定另一可用網路名稱的方法之一，是將它加入本機主機檔案。 本機主機檔案預設位於 WINDOWS\system32\drivers\etc 或 WINNT\system32\drivers\etc。如需詳細資訊，請參閱 Windows 文件集。  
  
     例如，若電腦名稱為 comp1，電腦 IP 位址是 10.193.17.129，且執行個體名稱為 inst1/instname，請將下列項目加入主機檔案：  
  
     10.193.17.129 inst1  
  
-   停用散發，註冊執行個體，然後重新建立散發。 如果 @@SERVERNAME 的值不是正確的非叢集執行個體值，請依循下列步驟：  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     執行 [sp_addserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql) 預存程序之後，您必須重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務，@@SERVERNAME 的變更才能生效。  
  
     如果 @@SERVERNAME 的值不是正確的非叢集執行個體值，則必須使用叢集管理員變更名稱。 如需詳細資訊，請參閱 < [ AlwaysOn 容錯移轉叢集執行個體 (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)。  
  
 在確認「散發者」執行個體已正確註冊之後，請確認散發資料庫是否列在 **msdb..MSdistributiondbs**中。 如果其沒有列在其中：  
  
1.  為散發組態編寫指令碼。 如需詳細資訊，請參閱 [Scripting Replication](scripting-replication.md)。  
  
2.  停用散發，然後再重新啟用它。 如需詳細資訊，請參閱 [Configure Distribution](configure-distribution.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
