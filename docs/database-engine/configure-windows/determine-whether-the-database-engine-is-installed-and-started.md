---
title: 判斷是否已安裝及啟動資料庫引擎 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, determining if installed
- verifying Database Engine installation
- viewing Database Engine installation
- installed Database Engine verification [SQL Server]
ms.assetid: babb02e4-3521-4b75-b5df-e09205594375
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 8f4e4af185f92d831be52bb714e05a848505ff2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66767647"
---
# <a name="determine-whether-the-database-engine-is-installed-and-started"></a>判斷是否已安裝及啟動 Database Engine
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  只要成功安裝 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，就會將檔案安裝至檔案系統、在登錄中建立項目並安裝許多工具。 此主題描述如何使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 組態管理員，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中確認 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否已安裝並啟動。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="how-to-view-and-start-the-database-engine-by-using-sql-server-configuration-manager"></a>如何使用 SQL Server 組態管理員來檢視並啟動 Database Engine  
  
1.  按一下 [開始]  ，依序指向 [所有程式]  、[Microsoft SQL Server]  和 [組態工具]  ，然後按一下 [SQL Server 組態管理員]  。  
  
     如果您在 [開始]  功能表上找不到這些項目，就表示未正確安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請執行安裝程式來安裝 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。  
  
2.  在 [SQL Server 組態管理員]  中，按一下左窗格中的 [SQL Server 服務]  。 右窗格會列出與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相關的許多服務。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 已安裝，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務就會列為 [SQL Server (MSSQLSERVER)]  (如果它是預設執行個體的話) 或 [SQL Server (\<*執行個體名稱*>)]   (如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 安裝成具名執行個體的話)。 除非執行個體名稱已變更，否則 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 會安裝為 **SQLEXPRESS** 名稱的具名執行個體。 綠色的三角形圖示是表示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 正在執行。 紅色的正方形圖示則表示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 已停止。  
  
3.  若要啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，請以滑鼠右鍵按一下右窗格中的 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，然後按一下 [啟動]  。  
  
> [!NOTE]  
>  在安裝過程中，使用者可以選取要用來安裝程式檔案和資料庫檔案的位置。 如果使用者接受預設位置，這些檔案就會安裝至 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)] 和 C:\Program Files\Microsoft SQL Server\MSSQL.*x*，其中 *x* 是數字。  
  
  
