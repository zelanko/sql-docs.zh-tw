---
title: "連接到 Microsoft Azure 儲存體 | Microsoft Docs"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-f1
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.windowsazurestorage.connect.f1
- SQL13.SWB.WINDOWSAZURESTORAGE.CONNECT.F1
ms.assetid: 
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b3f4019ad5eadcdd792586598c3cf93a4b0d1ce
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="connect-to-microsoft-azure-storage"></a>連接到 Microsoft Azure 儲存體
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 使用 [Windows Azure 儲存體連線] 對話方塊可以指定儲存體帳戶並且驗證 Windows Azure 的連線。  
  
## <a name="options"></a>選項。  
請指定有關 Windows Azure 帳戶的下列資訊，然後按一下 [下一步] 繼續進行。  
  
1.  **儲存體帳戶** - 指定儲存體帳戶名稱。

   >[!NOTE]
   > 您只能連線到[一般目的儲存體帳戶](https://docs.microsoft.com/en-us/azure/storage/storage-introduction#introducing-the-azure-storage-services)。 連線到其他類型的儲存體帳戶可能會造成類似下面的錯誤：
   >
   >  其中一個 HTTP 標頭之值的格式不正確。 (Microsoft.SqlServer.StorageClient)。
   >
   >  遠端伺服器傳回錯誤：(400) 錯誤的要求。 (系統)

2.  **帳戶金鑰** - 針對指定的儲存體帳戶指定帳戶金鑰。  
  
3.  **使用安全端點 (HTTPS)** - 這個選項會利用網路 Web 伺服器的加密通訊和安全識別。  
  
4.  **儲存帳戶金鑰** - 這個選項會將您的密碼儲存在加密的檔案中。  
  
