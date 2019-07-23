---
title: 連接到 Microsoft Azure 儲存體 (還原) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 84dfb4e9f5027650ae3a35146b13f70fd0f84a2e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076158"
---
# <a name="connect-to-microsoft-azure-storage-restore"></a>連接到 Microsoft Azure 儲存體 (還原)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此對話方塊可讓您指定 Windows Azure 儲存體帳戶資訊的連接，以擷取儲存在 Windows Azure 儲存體帳戶中的檔案。 指定必要資訊之後，按一下 [連接]  建立 Windows Azure 儲存體的連接。  
  
## <a name="windows-azure-storage-account"></a>Windows Azure 儲存體帳戶  
 **儲存體帳戶**  
 選取、輸入或貼上您想要使用的 Windows Azure 儲存體帳戶名稱。 下拉式方塊會列出先前使用的帳戶。  
  
 **帳戶金鑰**  
 指定 Windows Azure 儲存體帳戶存取金鑰。  
  
 [使用安全端點 (HTTPS)]  核取方塊  
 選取此選項，以確保 Microsoft Azure 儲存體的安全連線 (建議使用)。  
  
 [儲存帳戶金鑰]  核取方塊  
 如果您想要 SQL Server 記住此儲存體帳戶的存取金鑰，請選取此核取方塊。  
  
### <a name="sql-credential"></a>SQL 認證  
 **選取現有認證**  
 選取符合儲存體帳戶和帳戶金鑰資訊的現有 SQL 認證。  
  
 **建立新認證**  
 選取此選項，以使用儲存體帳戶和帳戶金鑰資訊建立新認證。 在 [認證名稱]  欄位中指定新認證的名稱。  
  
  
