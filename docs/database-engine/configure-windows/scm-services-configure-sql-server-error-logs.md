---
title: 設定 SQL Server 錯誤記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8e746861ef30305a901c388f7574a4a27e2edab4
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "74127486"
---
# <a name="scm-services---configure-sql-server-error-logs"></a>SCM 服務 - 設定 SQL Server 錯誤記錄檔

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何檢視或修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔的回收方式。  

## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>若要開啟 [設定 SQL Server 錯誤記錄檔] 對話方塊  

1. 在 [物件總管] 中展開 SQL Server 執行個體，展開 [管理]  ，以滑鼠右鍵按一下 [SQL Server 記錄檔]  ，然後按一下 [設定]  。

2. 在 **[設定 SQL Server 錯誤記錄檔]** 對話方塊中，從下列選項中進行選擇。

    a. 記錄檔計數

      **限制回收錯誤記錄檔之前，所允許的檔案數目**

      核取進行錯誤記錄檔的回收之前，可建立之錯誤記錄檔的數目。 每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，就會建立一個新的錯誤記錄檔。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會保留前六個記錄檔備份，除非您核取此選項，並在下面另行指定錯誤記錄檔的最大數目。  
  
      **錯誤記錄檔的最大數目**

      指定回收前建立的封存錯誤記錄檔數量上限。 預設為 6，不包括目前的記錄檔。 這個值會決定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在回收記錄檔前所保留的先前備份記錄數量。

    b. 記錄檔大小

      **錯誤記錄檔大小上限 (KB)**

      您可以設定每個檔案的大小量 (以 KB 為單位)。 如果您將其保留為 0，則記錄大小不受限制。
