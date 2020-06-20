---
title: 關於 SQL Server 資料庫引擎 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e3cf4ca5d422e9d124c397bbcae8d8b48d12b95b
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932726"
---
# <a name="about-the-sql-server-database-engine"></a>關於 SQL Server Database Engine
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件是用來儲存、處理及維護資料安全的核心服務。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 提供控制存取和快速交易處理，以符合企業中最需要的資料耗用應用程式的需求。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在單一電腦上最多支援 50 個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。 若要建立一般 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝，請參閱安裝[程式中的 Install SQL Server 2014 &#40;安裝&#41;](install-sql-server-from-the-installation-wizard-setup.md)。  
  
 **重要事項**若為本機安裝，您必須以系統管理員的身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。  
  
 當您在安裝精靈的 [要安裝的元件] 頁面上選取 [ ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫引擎**] 時，會安裝下列功能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   複寫 (選擇性元件)  
  
-   全文檢索搜尋 (選擇性元件)  
  
-   Data Quality Services (選擇性元件)  
  
    > [!NOTE]  
    >  在這版的安裝程式中選取 [Data Quality Services]**** 核取方塊，並不會安裝 Data Quality Services (DQS) 伺服器。 您必須執行額外的安裝後步驟，才能安裝 DQS 伺服器。 如需詳細資訊，請參閱 [安裝 Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)。  
  
 下列其他功能是許多典型使用者案例的選項：  
  
-   Data Quality Client  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   連接元件  
  
-   程式設計模型  
  
-   管理工具  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   文件集元件  
  
> [!NOTE]  
>  根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程序中不會安裝範例資料庫和範例程式碼。 若要安裝範例資料庫和範例程式碼，請參閱 [CodePlex 網站](https://go.microsoft.com/fwlink/?LinkId=87843)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [SQL Server 2014 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)   
 [高可用性解決方案 &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [使用安裝精靈 &#40;安裝程式升級至 SQL Server 2014&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
