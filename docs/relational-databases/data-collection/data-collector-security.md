---
title: "資料收集器安全性 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data collection [SQL Server]
- security [data collector]
- data collector [SQL Server], security
ms.assetid: e75d6975-641e-440a-a642-cb39a583359a
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 62b958f5a1c032e11b5aaef37692b5de21a0bec4
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="data-collector-security"></a>資料收集器安全性
  資料收集器會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式所實作之以角色為基礎的安全性模型。 這個模型可讓資料庫管理員在只具有執行該工作所需權限的安全性內容中執行各種資料收集器工作。 這個方法也可用於牽涉到內部資料表的作業，這些資料表只能使用預存程序或檢視來存取。 系統不會授與任何權限給內部資料表。 不過，系統會針對用來存取資料表之預存程序或檢視表的使用者檢查權限。  
  
> [!IMPORTANT]  
>  此安全性模型的另一個重要層面為同心權限。 在同心權限之下，較高權限的角色會繼承較低權限的角色在物件上的權限 (包括警示、操作員、作業、排程和 Proxy)。 如需詳細資訊，請參閱 [SQL Server Agent Fixed Database Roles](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 下列章節將大略描述資料收集安全性，以及您必須授與給使用者的角色，好讓您可以設定及使用資料收集器，並執行與管理資料倉儲有關的工作。  
  
## <a name="general-security"></a>一般安全性  
 資料收集器的安裝是根據針對 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]所指定的記載標準。  
  
### <a name="network-security"></a>網路安全性  
 機密資訊可以在目標執行個體、與組態伺服器有關的關聯式執行個體、執行中的收集組，以及主控管理資料倉儲的伺服器之間傳遞。  
  
 為了保護透過網路傳輸的任何資料，會實作標準安全性機制，例如 [!INCLUDE[tsql](../../includes/tsql-md.md)]的通訊協定加密。  
  
## <a name="permissions-for-configuring-and-using-the-data-collector"></a>設定及使用資料收集器的權限  
 根據工作而定，使用者必須是針對資料收集器提供之一個或多個固定資料庫角色的成員。 下面依照最高存取權限到最低存取權限的順序列出這些角色：  
  
-   **dc_admin**  
  
-   **dc_operator**  
  
-   **dc_proxy**  
  
 這些角色儲存在 msdb 資料庫中。 根據預設，沒有任何使用者隸屬於這些資料庫角色的成員。 您必須明確授與這些角色的使用者成員資格。  
  
 屬於 **系統管理員 (sysadmin)** 固定伺服器角色的使用者將擁有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 物件和資料收集器檢視表的完整存取權。 不過，您必須將他們明確加入至資料收集器角色。  
  
> [!IMPORTANT]  
>  db_ssisadmin 角色和 dc_admin 角色的成員可以將其權限提高為系統管理員 (sysadmin)。 之所以能夠進行此權限提高，是因為這些角色可以修改 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，而且 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可藉由使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的 sysadmin 安全性內容由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行。 若要在執行維護計畫、資料收集組和其他 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝時預防此權限提高，請將執行封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業設為使用有限權限的 Proxy 帳戶，或是只將系統管理員 (sysadmin) 成員加入 db_ssisadmin 和 dc_admin 角色。  
  
### <a name="dcadmin-role"></a>dc_admin 角色  
 指派給 **dc_admin** 角色的使用者對於伺服器執行個體上的資料收集器組態具有完整系統管理員存取權 (建立、讀取、更新和刪除)。 這個角色的成員可以執行以下作業：  
  
-   設定收集器層級的屬性。  
  
-   加入新的收集組。  
  
-   安裝新的集合類型。  
  
-   執行 **dc_operator** 角色允許的所有作業。  
  
 **dc_admin** 角色是下列角色的成員：  
  
-   **SQLAgentUserRole**。 這個角色是建立排程及執行作業所需的角色。  
  
    > [!NOTE]  
    >  針對資料收集器所建立的 Proxy 必須授與 **dc_admin** 的存取權，才能建立 Proxy 並將 Proxy 用於需要 Proxy 的任何作業步驟。  
  
-   **dc_operator**。 **dc_admin** 的成員會繼承提供給 **dc_operator**的權限。  
  
### <a name="dcoperator-role"></a>dc_operator 角色  
 **dc_operator** 角色的成員具有讀取和更新的存取權。 這個角色支援與執行和設定收集組有關的作業工作。 這個角色的成員可以執行以下作業：  
  
-   啟動或停止收集組。  
  
-   列舉現有的收集組。  
  
-   檢視與收集組有關的詳細資訊 (例如集合項目和收集頻率)。  
  
-   變更現有收集組的上傳頻率。  
  
-   針對屬於現有收集組之一部分的集合項目變更其收集頻率。  
  
 **dc_operator** 角色是列舉及檢視資料收集器封裝時所需下列角色的成員：  
  
-   **db_ssisltduser**  
  
-   **db_ssisoperator**  
  
 如需詳細資訊，請參閱 [Integration Services 角色 &#40;SSIS 服務&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)。  
  
### <a name="dcproxy-role"></a>dc_proxy 角色  
 **dc_proxy** 角色的成員對於資料收集器收集組和收集器層級的屬性具有讀取存取權。 這個角色的成員也可以執行自己所擁有的作業，並建立以現有 Proxy 帳戶身分執行的作業步驟。  
  
 這個角色的成員可以執行以下作業：  
  
-   檢視收集組組態資訊 (例如集合項目的輸入參數及這些項目的收集頻率)。  
  
-   取得只能由單一預存程序存取的內部加密資訊 (例如，用於資料上傳的資料倉儲連接資訊)。  
  
-   記錄收集組執行階段事件。  
  
 **dc_proxy** 角色是列舉及檢視資料收集器封裝時所需下列角色的成員：  
  
-   **db_ssisltduser**。  
  
-   **db_ssisoperator**  
  
 如需詳細資訊，請參閱 [Integration Services 角色 &#40;SSIS 服務&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)。  
  
## <a name="permissions-for-configuring-and-using-the-management-data-warehouse"></a>設定及使用管理資料倉儲的權限  
 根據工作而定，使用者必須是針對存取管理資料倉儲所提供之一個或多個固定資料庫角色的成員。 下面依照最高存取權限到最低存取權限的順序列出這些角色：  
  
-   **mdw_admin**  
  
-   **mdw_writer**  
  
-   **mdw_reader**  
  
 這些角色儲存在 msdb 資料庫中。 根據預設，沒有任何使用者隸屬於這些資料庫角色的成員。 您必須明確授與這些角色的使用者成員資格。  
  
 屬於 **系統管理員 (sysadmin)** 固定伺服器角色的使用者將擁有資料收集器檢視表的完整存取權。 不過，您必須將他們明確加入至資料庫角色，才能執行其他作業。  
  
### <a name="mdwadmin-role"></a>mdw_admin 角色  
 **mdw_admin** 角色的成員對於管理資料倉儲具有讀取、寫入、更新和刪除的存取權。  
  
 這個角色的成員可以執行以下作業：  
  
-   在需要時變更管理資料倉儲結構描述 (例如，在安裝新的集合類型時加入新的資料表)。  
  
    > [!NOTE]  
    >  當結構描述變更時，使用者也必須是 **dc_admin** 角色的成員，才能安裝新的收集器型別，因為這個動作需要在 msdb 中擁有更新資料收集器組態的權限。  
  
-   在管理資料倉儲上執行維護作業，例如封存或清除。  
  
### <a name="mdwwriter-role"></a>mdw_writer 角色  
 **mdw_writer** 角色的成員可以將資料上傳及寫入管理資料倉儲。 在管理資料倉儲內儲存資料的任何資料收集器都必須是這個角色的成員。  
  
### <a name="mdwreader-role"></a>mdw_reader 角色  
 **mdw_reader** 角色的成員對於管理資料倉儲具有讀取存取權。 由於這個角色的目的是要藉由提供歷程記錄資料的存取來支援疑難排解，所以這個角色的成員無法檢視管理資料倉儲結構描述的其他元素。  
  
## <a name="see-also"></a>另請參閱  
 [實作 SQL Server Agent 安全性](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)  
  
  
