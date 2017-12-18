---
title: "連接到 Microsoft Azure 儲存體 (還原) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c1e0129c986da132733fc102358229a64e5fbf77
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="connect-to-microsoft-azure-storage-restore"></a>連接到 Microsoft Azure 儲存體 (還原)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 此對話方塊可讓您指定 Windows Azure 儲存體帳戶資訊的連線，以擷取儲存在 Windows Azure 儲存體帳戶中的檔案。 指定必要資訊之後，按一下 [連接] 建立 Windows Azure 儲存體的連接。  
  
## <a name="windows-azure-storage-account"></a>Windows Azure 儲存體帳戶  
 **儲存體帳戶**  
 選取、輸入或貼上您想要使用的 Windows Azure 儲存體帳戶名稱。 下拉式方塊會列出先前使用的帳戶。  
  
 **帳戶金鑰**  
 指定 Windows Azure 儲存體帳戶存取金鑰。  
  
 [使用安全端點 (HTTPS)] 核取方塊  
 選取此選項，以確保 Windows Azure 儲存體的安全連接 (建議使用)。  
  
 [儲存帳戶金鑰]核取方塊  
 如果您想要 SQL Server 記住此儲存體帳戶的存取金鑰，請選取此核取方塊。  
  
### <a name="sql-credential"></a>SQL 認證  
 **選取現有認證**  
 選取符合儲存體帳戶和帳戶金鑰資訊的現有 SQL 認證。  
  
 **建立新認證**  
 選取此選項，以使用儲存體帳戶和帳戶金鑰資訊建立新認證。 在 [認證名稱] 欄位中指定新認證的名稱。  
  
  
