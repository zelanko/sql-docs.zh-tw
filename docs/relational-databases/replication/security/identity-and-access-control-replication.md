---
title: "識別和存取控制 (複寫) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "存取控制 [SQL Server 複寫]"
  - "安全性 [SQL Server 複寫], 識別和存取控制"
  - "驗證 [SQL Server 複寫]"
  - "識別 [複寫]"
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
caps.latest.revision: 8
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# 識別和存取控制 (複寫)
  驗證是程序的實體 （通常在此內容中的電腦） 驗證該另一個實體，也稱為 *主體*, ，（通常是另一部電腦或使用者） 是人員或其本身宣稱。 授權是向已驗證的主體授與資源 (例如檔案系統中的檔案或是資料庫中的資料表) 存取權的處理。  
  
 複寫安全性使用驗證與授權來控制對複寫資料庫物件，以及複寫處理所涉及的電腦和代理程式的存取權限。 這可透過三種機制來完成：  
  
-   代理程式安全性  
  
     複寫代理程式安全性模型允許精確控制複寫代理程式執行並建立連接所使用的帳戶。 如需代理程式安全性模型的詳細資訊，請參閱 [複寫代理程式安全性模型](../../../relational-databases/replication/security/replication-agent-security-model.md)。 代理程式設定登入和密碼的相關資訊，請參閱 [管理登入和密碼的複寫](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)。  
  
-   管理角色  
  
     確定複寫設定、維護及處理所使用的是正確的伺服器和資料庫角色。 如需詳細資訊，請參閱 [複寫的安全性角色需求](../../../relational-databases/replication/security/security-role-requirements-for-replication.md)。  
  
-   發行集存取清單 (PAL)   
  
     透過 PAL 授與發行集存取權限。 PAL 功能類似於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 存取控制清單。 當「訂閱者」連接到「發行者」或「散發者」，並要求存取發行集時，代理程式傳送的驗證資訊會依據 PAL 來進行檢查。 如需詳細資訊與 PAL 的最佳作法，請參閱 [保護發行者](../../../relational-databases/replication/security/secure-the-publisher.md)。  
  
## 篩選發行的資料  
 除了使用驗證和授權來控制對複寫資料及物件的存取外，複寫還含有兩個選項可用於控制訂閱者端可用的資料：資料行篩選和資料列篩選。 如需篩選的詳細資訊，請參閱 [篩選已發佈資料](../../../relational-databases/replication/publish/filter-published-data.md)。  
  
 定義發行項時，您可以只發行發行集所需的資料行，而省略不需要或含有機密資料的資料行。 例如，當發行 **客戶** 資料表從欄位中的銷售代表 Adventure Works 資料庫，您可以省略 **AnnualSales** 可能只與公司相關資料行。  
  
 篩選發行的資料允許您對資料存取進行限制，並允許您指定「訂閱者」上可用的資料。 例如，您可以篩選 **客戶** 資料表，以便讓公司合作夥伴僅收到客戶的相關資訊的 **ShareInfo** 資料行的值為 [是]。 對於合併式複寫，如果使用含有 HOST_NAME() 的參數化篩選，則有安全性考量。 如需詳細資訊，請參閱 「 使用 host_name （） 篩選 」 一節中 [參數化資料列篩選](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
## 另請參閱  
 [安全性和保護 & #40。複寫 & #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [安全性概觀與 #40。複寫 & #41;](../../../relational-databases/replication/security/security-overview-replication.md)   
 [威脅和弱點安全防護 & #40。複寫 & #41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md)  
  
  