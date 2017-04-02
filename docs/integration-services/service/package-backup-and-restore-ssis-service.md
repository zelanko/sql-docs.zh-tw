---
title: "封裝備份和還原 (SSIS 服務) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SSIS 封裝, 備份和還原"
  - "備份封裝 [Integration Services]"
  - "封裝 [Integration Services], 備份和還原"
  - "SQL Server Integration Services 封裝, 備份和還原"
  - "還原封裝 [Integration Services]"
  - "Integration Services 封裝, 備份和還原"
ms.assetid: c67d3b83-a6c8-40de-920f-9236de4ac87f
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# 封裝備份和還原 (SSIS 服務)
    
> [!IMPORTANT]  
>  本主題會討論 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務，即用於管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的 Windows 服務。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 支援此服務能與舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]回溯相容。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始，您可以管理 Integration Services 伺服器上的物件，例如封裝。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝可以儲存至檔案系統或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫 msdb。 儲存至 msdb 的封裝可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份和還原功能進行備份和還原。  
  
 如需備份和還原 msdb 資料庫的詳細資訊，請按一下下列主題之一：  
  
-   [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [系統資料庫的備份與還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含可用來管理封裝的 **dtutil** 命令提示公用程式 (dtutil.exec)。 如需詳細資訊，請參閱 [dtutil Utility](../../integration-services/dtutil-utility.md)。  
  
## 組態檔  
 封存包含的所有組態檔都儲存在檔案系統中。 備份 msdb 資料庫時並不會備份這些檔案；因此，作為儲存至 msdb 之封裝保護計畫的一部份，您應確保定期備份組態檔。 若要在 msdb 資料庫的備份中包含組態，應考慮使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態類型而不是以檔案為基礎的組態。  
  
## 儲存在檔案系統中的封裝  
 儲存至檔案系統之封裝的備份應納入備份伺服器檔案系統的計畫中。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務組態檔 (預設名稱為 MsDtsSrvr.ini.xml) 會列出服務監視之伺服器上的資料夾。 您應確定已備份這些資料夾。 另外，封裝也可能儲存在伺服器上的其他資料夾中，您應確保在備份中包含這些資料夾。  
  
  