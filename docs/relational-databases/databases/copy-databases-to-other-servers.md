---
title: "複製資料庫至其他伺服器 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- servers [SQL Server], copying databases between
- bulk exporting [SQL Server], between servers
- database copying [SQL Server]
- migrating databases [SQL Server]
- moving databases
- copying databases
- bulk importing [SQL Server], between servers
ms.assetid: 978406d6-a3c8-4902-b1f4-4ced75234be5
caps.latest.revision: "42"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4f3b75305cf6db462e099d1a2a752bbca6014826
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="copy-databases-to-other-servers"></a>複製資料庫至其他伺服器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 有時候，將資料庫從某部電腦複製到另一部電腦很有用，包括測試、一致性檢查、開發軟體、執行報表、建立鏡像資料庫，或讓資料庫可用於遠端分支作業。  
  
 複製資料庫的方式有許多種：  
  
-   使用複製資料庫精靈  
  
     您可以使用「複製資料庫精靈」在伺服器之間複製或移動資料庫，或將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫升級至更新版本。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
-   還原資料庫備份  
  
     若要複製整個資料庫，您可以使用 BACKUP 與 RESTORE [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 還原資料庫的完整備份，可用來將某部電腦的資料庫複製到另一部上，而會這麼做通常有許多原因。 如需使用備份與還原來複製資料庫的資訊，請參閱[使用備份與還原複製資料庫](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)。  
  
    > [!NOTE]  
    >  若要設定鏡像資料庫以執行資料庫鏡像作業，您必須使用 RESTORE DATABASE *<資料庫名稱>* WITH NORECOVERY 將資料庫還原成鏡像伺服器。 如需詳細資訊，請參閱[準備鏡像資料庫以進行鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)。  
  
-   使用產生指令碼精靈來發行資料庫  
  
     您可以使用產生指令碼精靈，將某個資料庫從本機電腦傳送至 Web 主控提供者。 如需詳細資訊，請參閱 [產生和發佈指令碼精靈](../../relational-databases/scripting/generate-and-publish-scripts-wizard.md)。  
  
  
