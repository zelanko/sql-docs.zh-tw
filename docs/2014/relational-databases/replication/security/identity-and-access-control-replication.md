---
title: 識別和存取控制 (複寫) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- access controls [SQL Server replication]
- security [SQL Server replication], identity and access control
- authentication [SQL Server replication]
- identity [Replication]
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c5e1940ffefda1df26bfd2221bf6bcbeb0727bf3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056874"
---
# <a name="identity-and-access-control-replication"></a>識別和存取控制 (複寫)
  驗證是某一實體 (在本文中通常是某台電腦) 驗證另一個實體 (通常是另一台電腦或使用者) 的身分或所代表身分的處理，實體也稱為 *「主體」* 。 授權是向已驗證的主體授與資源 (例如檔案系統中的檔案或是資料庫中的資料表) 存取權的處理。  
  
 複寫安全性使用驗證與授權來控制對複寫資料庫物件，以及複寫處理所涉及的電腦和代理程式的存取權限。 這可透過三種機制來完成：  
  
-   代理程式安全性：複寫代理程式安全性模型可讓您更精細地控制複寫代理程式執行和連接所用的帳戶。 如需代理程式安全性模型的詳細資訊，請參閱＜ [Replication Agent Security Model](replication-agent-security-model.md)＞。 如需設定代理程式登入和密碼的資訊，請參閱[管理複寫的登入與密碼](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)。  
  
-   系統管理角色：確定已使用正確的伺服器和資料庫角色進行複寫設定、維護和處理。 如需詳細資訊，請參閱 [Security Role Requirements for Replication](security-role-requirements-for-replication.md)。  
  
-   發行集存取清單（PAL）：透過 PAL 授與發行集的存取權。 PAL 功能類似於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 存取控制清單。 當「訂閱者」連接到「發行者」或「散發者」，並要求存取發行集時，代理程式傳送的驗證資訊會依據 PAL 來進行檢查。 如需 PAL 的詳細資訊和最佳做法，請參閱[保護發行者](secure-the-publisher.md)。  
  
## <a name="filtering-published-data"></a>篩選發行的資料  
 除了使用驗證和授權來控制對複寫資料及物件的存取外，複寫還含有兩個選項可用於控制訂閱者端可用的資料：資料行篩選和資料列篩選。 如需篩選的詳細資訊，請參閱[篩選發行的資料](../publish/filter-published-data.md)。  
  
 定義發行項時，您可以只發行發行集所需的資料行，而省略不需要或含有機密資料的資料行。 例如，向現場的銷售代表發行 Adventure Works 資料庫的 **Customer** 資料表時，可以省略 **AnnualSales** 資料行，這行僅與公司管理者有關。  
  
 篩選發行的資料允許您對資料存取進行限制，並允許您指定「訂閱者」上可用的資料。 例如，您可以篩選 **Customer** 資料表，以便讓公司合作夥伴僅收到 **ShareInfo** 資料行值為「yes」之客戶的相關資訊。 對於合併式複寫，如果使用含有 HOST_NAME() 的參數化篩選，則有安全性考量。 如需詳細資訊，請參閱＜ [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)＞中的「使用 HOST_NAME() 進行篩選」一節。  

## <a name="manage-logins-and-passwords-in-replication"></a>管理複寫的登入與密碼
  設定複寫時請指定複寫代理程式的登入與密碼。 設定複寫後，您可以變更登入與密碼。 如需詳細資訊，請參閱 [View and Modify Replication Security Settings](view-and-modify-replication-security-settings.md)。 若要變更複寫代理程式使用之帳戶的密碼，請執行 [sp_changereplicationserverpasswords &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式安全性模型](replication-agent-security-model.md)   
 [複寫安全性最佳作法](replication-security-best-practices.md)   
 [SQL Server 複寫安全性](view-and-modify-replication-security-settings.md)   
 [複寫威脅和弱點緩和措施](threat-and-vulnerability-mitigation-replication.md)   

  
  
