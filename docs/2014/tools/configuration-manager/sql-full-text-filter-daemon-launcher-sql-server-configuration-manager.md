---
title: SQL 全文檢索篩選精靈啟動器 (SQL Server 設定管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- configmgr-client
ms.topic: conceptual
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca40d5db19ef4f24e93af444a0ef8c2e7179b159
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169928"
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>SQL 全文檢索篩選背景程式啟動器 (SQL Server 組態管理員)
  從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]開始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文檢索搜尋就會使用 SQL 全文檢索篩選背景程式啟動器 (FDHOST 啟動器) 服務來啟動篩選背景程式主機處理序，以便處理全文檢索搜尋篩選和斷詞。 若要使用全文檢索搜尋，您必須執行這個服務。 FDHOST 啟動器服務是一個與特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體有關的執行個體感知服務。 FDHOST 啟動器服務會將服務帳戶資訊傳播至啟動的每個篩選背景程式主機處理序。 如需篩選背景程式主機處理序的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜全文檢索搜尋架構＞。  
  
  
