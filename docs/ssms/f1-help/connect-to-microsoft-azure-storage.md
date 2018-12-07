---
title: 連接到 Microsoft Azure 儲存體 | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.windowsazurestorage.connect.f1
- SQL13.SWB.WINDOWSAZURESTORAGE.CONNECT.F1
ms.assetid: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cd9af00c06b2e999ec38d201e11fe305f7bb4e71
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523575"
---
# <a name="connect-to-microsoft-azure-storage"></a>連接到 Microsoft Azure 儲存體
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
使用 [Windows Azure 儲存體連接] 對話方塊可以指定儲存體帳戶並且驗證 Windows Azure 的連接。  
  
## <a name="options"></a>選項。  
請指定有關 Windows Azure 帳戶的下列資訊，然後按一下 [下一步] 繼續進行。  
  
1.  **儲存體帳戶** - 指定儲存體帳戶名稱。

   >[!NOTE]
   > 您只能連線到[一般目的儲存體帳戶](https://docs.microsoft.com/azure/storage/storage-introduction#introducing-the-azure-storage-services)。 連線到其他類型的儲存體帳戶可能會造成類似下面的錯誤：
   >
   >  其中一個 HTTP 標頭之值的格式不正確。 (Microsoft.SqlServer.StorageClient)。
   >
   >  遠端伺服器傳回錯誤：(400) 錯誤的要求。 (系統)

2.  **帳戶金鑰** - 針對指定的儲存體帳戶指定帳戶金鑰。  
  
3.  **使用安全端點 (HTTPS)** - 這個選項會利用網路 Web 伺服器的加密通訊和安全識別。  
  
4.  **儲存帳戶金鑰** - 這個選項會將您的密碼儲存在加密的檔案中。  
  
