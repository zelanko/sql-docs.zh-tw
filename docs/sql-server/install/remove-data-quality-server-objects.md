---
title: 移除 Data Quality Server 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1b7c6dbb-b40e-4822-9caa-608e1056af8e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 103193bc2e9f8b487a2f7083b09cf0f2f856e869
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993400"
---
# <a name="remove-data-quality-server-objects"></a>移除 Data Quality Server 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  從 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 執行個體解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或完整移除內含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 執行個體時，不會刪除某些 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 物件，包括 DQS 資料庫。 這意味著如果您使用 SQL Server 安裝程式解除安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] ，就不會失去 DQS 資料。 您必須在完成解除安裝程序之後，手動刪除這些 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 物件。  
  
> [!NOTE]  
>  -   解除安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]之前，請考慮將所有現有的知識庫匯出到 .dqsb 檔加以備份，並於之後使用該檔案將所有知識庫匯入到新的 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安裝中。 您只能透過在命令提示字元中，執行 DQSInstaller.exe 搭配適當命令列參數的方式匯出和匯入所有 DQS 知識庫。 如需詳細資訊，請參閱 [Export and Import DQS Knowledge Bases Using DQSInstaller.exe](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)。  
> -   刪除 DQS 資料庫之前，如果您要保留資料庫，請考慮備份該資料庫，並在稍後用於還原資料。 如需執行此作業的相關資訊，請參閱 [管理 DQS 資料庫](../../data-quality-services/manage-dqs-databases.md)。  
  
## <a name="uninstall-data-quality-server-from-a-sql-server-instance"></a>從 SQLServer 執行個體解除安裝資料品質伺服器  
 如果您只要從 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 執行個體解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您必須在完成 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 的解除安裝程序之後，手動從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體刪除下列 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 物件：  
  
-   DQS_MAIN、DQS_PROJECTS 和 DQS_STAGING_DATA 資料庫。  
  
-   \##MS_dqs_db_owner_login## 和 ##MS_dqs_service_login## 登入。  
  
-   master 資料庫中的 DQInitDQS_MAIN 預存程序。  
  
 您可以滑鼠右鍵按一下物件，然後按一下快速鍵功能表中的 [刪除] 來刪除 SQL Server Management Studio 中的這些物件。  
  
> [!IMPORTANT]  
>  如果您只要使用 `–uninstall` 命令列參數解除安裝 SQL Server 執行個體中的 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]，則在解除安裝過程中將刪除所有 DQS 物件。 您不必在解除安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]之後手動刪除這些物件。 若要從命令提示字元解除安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] ，請在命令提示字元中輸入下列命令，然後按 ENTER：   
> `dqsinstaller.exe -uninstall`  
  
## <a name="uninstall-sql-server-instance-containing-data-quality-server"></a>解除安裝包含資料品質伺服器的 SQL Server 執行個體  
 如果您要完整解除安裝內含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]執行個體，必須在完成解除安裝程序之後，手動刪除電腦中的 DQS_MAIN、DQS_PROJECTS 及 DQS_STAGING_DATA 資料庫。 針對預設的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝，DQS_MAIN、DQS_PROJECTS 和 DQS_STAGING_DATA 資料庫檔案位於 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA。  
  
## <a name="see-also"></a>另請參閱  
 [解除安裝現有的 SQL Server 執行個體 &#40;Setup&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)   
 [解除安裝 SQL Server 2016](../../sql-server/install/uninstall-sql-server.md)  
  
  
