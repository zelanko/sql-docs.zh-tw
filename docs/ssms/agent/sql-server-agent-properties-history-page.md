---
title: "SQL Server Agent 屬性 (記錄頁面) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 624f225d6ee4f8b00831f1ce0201538c5047e60e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-agent-properties-history-page"></a>SQL Server Agent 屬性 (記錄頁面)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 使用此頁面來檢視和修改管理 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務記錄的設定。  
  
## <a name="options"></a>選項。  
**限制作業記錄大小**  
對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 在記錄中所保留的作業記錄資訊量加以設限。  
  
**作業記錄大小上限 (以資料列為單位)**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會保留的最大資料列數目。 當記錄成長至此資料列數目時，隨著新資料列的輸入， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會移除記錄中最舊的資料列。  
  
**每項作業的作業記錄最大資料列數**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會為每項作業保留的最大資料列數目。 當特定作業的記錄成長至此資料列數目時，隨著新資料列的輸入， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會移除記錄中最舊的資料列。  
  
**移除代理程式記錄**  
指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會移除已存在於記錄中超過指定時間長度的項目。 這是單次移除記錄的執行作業。 如果需要重複的作業，請建立並排程含有清除作業的維護計畫。  
  
**早於**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會保留項目的時間。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server Agent 錯誤記錄檔](../../ssms/agent/sql-server-agent-error-log.md)  
  
