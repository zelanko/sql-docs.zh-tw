---
title: MSSQL_ENG014114 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014114 error
ms.assetid: f5f04590-e1c6-40d8-ab2b-98c791a0fc44
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3ba2a1fde59f55eecbfeeec46555567cde964f8d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049302"
---
# <a name="mssql_eng014114"></a>MSSQL_ENG014114
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|14114|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|'%s' 並未設定為散發者。|  
  
## <a name="explanation"></a>說明  
 如果錯誤訊息指定了特定的執行個體而非 'null'，則指定的執行個體尚未正確設定，以識別為「散發者」。  
  
 如果訊息指定 'null' 為「散發者」，則 **master** 資料庫中沒有本機伺服器的項目，或者項目不正確 (可能因為電腦已重新命名)。 針對拓撲中所有伺服器，複寫預計應使用電腦名稱與選擇性的執行個體名稱註冊 (叢集執行個體則為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 虛擬伺服器名稱加上選擇性的執行個體名稱)。 要讓複寫正常運作， `SELECT @@SERVERNAME` 針對拓撲中每部伺服器傳回的值，都應該符合電腦名稱或虛擬伺服器名稱加上選擇性執行個體名稱。  
  
 若您已透過 IP 位址或完整格式的網域名稱 (FQDN) 註冊任一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，就不支援複寫。 如果您設定複寫時，依 IP 位址或依 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 FQDN 註冊了任何 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 執行個體，就可能會引發這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
 如果錯誤訊息指定了特定的執行個體，請將伺服器設定為「散發者」。 如需詳細資訊，請參閱 [Configure Distribution](configure-distribution.md)＞。  
  
 如果訊息未指定特定執行個體 ('null')，請確認「散發者」執行個體已正確註冊。 若電腦網路名稱和 SQL Server 執行個體名稱不符，則：  
  
-   加入 SQL Server 執行個體名稱做為有效網路名稱。 設定另一可用網路名稱的方法之一，是將它加入本機主機檔案。 本機主機檔案預設位於 WINDOWS\system32\drivers\etc 或 WINNT\system32\drivers\etc。如需進一步資訊，請參閱 Windows 文件集。  
  
     例如，若電腦名稱為 comp1，電腦 IP 位址是 10.193.17.129，且執行個體名稱為 inst1/instname，請將下列項目加入主機檔案：  
  
     10.193.17.129 inst1  
  
-   停用散發，註冊執行個體，然後重新建立散發。 如果 @@SERVERNAME 的值對非叢集執行個體並不正確，請遵循下列步驟進行：  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     執行 [sp_addserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql) 預存程序之後，您必須重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務，@@SERVERNAME 的變更才能生效。  
  
     如果 @@SERVERNAME 的值不是正確的非叢集執行個體值，則必須使用叢集管理員變更名稱。 如需詳細資訊，請參閱 [AlwaysOn 容錯移轉叢集執行個體 (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
