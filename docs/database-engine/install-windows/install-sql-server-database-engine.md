---
title: "安裝 SQL Server Database Engine | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Database Engine [SQL Server], 安裝"
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
caps.latest.revision: 45
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 45
---
# 安裝 SQL Server Database Engine
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件是用來儲存、處理及維護資料安全的核心服務。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 提供控制存取和快速交易處理，以符合企業中最需要的資料耗用應用程式的需求。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在單一電腦上最多支援 50 個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。 若要建立一般的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝，請參閱[從安裝精靈 &#40;安裝程式&#41; 安裝 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)。  
  
 **重要事項**若為本機安裝，您必須以系統管理員的身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。  
  
 當您在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈] 的 [要安裝的元件] 頁面上選取 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Engine] 時，會安裝下列功能：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   複寫 (選擇性元件)  
  
-   全文檢索搜尋 (選擇性元件)  
  
-   Data Quality Services (選擇性元件)  
  
    > [!NOTE]  
    >  在這一版的安裝程式中選取 [Data Quality Services] 核取方塊，並不會安裝 Data Quality Services (DQS) 伺服器。 您必須執行額外的安裝後步驟，才能安裝 DQS 伺服器。 如需詳細資訊，請參閱[安裝 Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)。  
  
 下列其他功能是許多典型使用者案例的選項：  
  
-   Data Quality Client  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   連接元件  
  
-   程式設計模型  
  
-   管理工具  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   文件集元件  
  
> [!NOTE]  
>  根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程序中不會安裝範例資料庫和範例程式碼。 若要安裝範例資料庫和範例程式碼，請參閱 [CodePlex 網站](http://go.microsoft.com/fwlink/?LinkId=87843)。  
  
## 另請參閱  
 [SQL Server 2016 版本支援的功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)   
 [SQL Server 2016 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)   
 [高可用性解決方案 &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [使用安裝精靈升級為 SQL Server 2016 &#40;安裝程式&#41;](../../database-engine/install-windows/upgrade-to-sql-server-2016-using-the-installation-wizard-setup.md)  
  
  