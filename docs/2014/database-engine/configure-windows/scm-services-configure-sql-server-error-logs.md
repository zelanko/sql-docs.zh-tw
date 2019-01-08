---
title: 設定 SQL Server 錯誤記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 60d38caf365d6db54ea0abe688a3fc2979fdab82
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2018
ms.locfileid: "52639476"
---
# <a name="configure-sql-server-error-logs"></a>設定 SQL Server 錯誤記錄檔
  此主題描述如何檢視或修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔的回收方式。  
  
## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>若要開啟 [設定 SQL Server 錯誤記錄檔] 對話方塊  
  
1.  在 [物件總管] 中展開 SQL Server 執行個體，展開 [管理]，以滑鼠右鍵按一下 [SQL Server 記錄檔]，然後按一下 [設定]。  
  
2.  在 **[設定 SQL Server 錯誤記錄檔]** 對話方塊中，從下列選項中進行選擇。  
  
     **限制回收錯誤記錄檔之前，所允許的檔案數目**  
     核取進行錯誤記錄檔的回收之前，可建立之錯誤記錄檔的數目。 每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，就會建立一個新的錯誤記錄檔。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會保留前六個記錄檔備份，除非您核取此選項，並在下面另行指定錯誤記錄檔的最大數目。  
  
     **錯誤記錄檔的最大數目**  
     指定回收之前建立之錯誤記錄檔的最大數目。 預設值是 6，這是回收錯誤記錄檔之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保留的先前備份記錄檔數目。  
  
  
