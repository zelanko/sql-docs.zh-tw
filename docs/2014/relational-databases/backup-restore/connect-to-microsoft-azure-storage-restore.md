---
title: 連接到 Azure 儲存體（還原） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9fb4a8943c237e37ca612bf367abe99d47c8eb08
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84958783"
---
# <a name="connect-to-azure-storage-restore"></a>連線到 Azure 儲存體 (還原)
  此對話方塊可讓您指定 Azure 儲存體帳戶資訊的連線，以擷取儲存在 Azure 儲存體帳戶中的檔案。 指定必要資訊之後，按一下 [連接]  建立 Azure 儲存體的連線。  
  
## <a name="azure-storage-account"></a>Azure 儲存體帳戶  
 **儲存體帳戶**  
 選取、輸入或貼上您想要使用的 Azure 儲存體帳戶名稱。 下拉式方塊會列出先前使用的帳戶。  
  
 **帳戶金鑰**  
 指定 Azure 儲存體帳戶存取金鑰。  
  
 [使用安全端點 (HTTPS)]  核取方塊  
 選取此選項，以確保 Azure 儲存體的安全連線 (建議使用)。  
  
 [儲存帳戶金鑰]  核取方塊  
 如果您想要 SQL Server 記住此儲存體帳戶的存取金鑰，請選取此核取方塊。  
  
### <a name="sql-credential"></a>SQL 認證  
 **選取現有認證**  
 選取符合儲存體帳戶和帳戶金鑰資訊的現有 SQL 認證。  
  
 **建立新認證**  
 選取此選項，以使用儲存體帳戶和帳戶金鑰資訊建立新認證。 在 [認證名稱]  欄位中指定新認證的名稱。  
  
  
