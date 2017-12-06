---
title: "SQL 全文檢索篩選背景程式啟動器 （SQL Server 組態管理員） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0829cbef976a5fc53166cf5616a900e8472e9e0d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>SQL 全文檢索篩選背景程式啟動器 (SQL Server 組態管理員)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]從開始[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，就會使用 SQL 全文檢索篩選背景程式啟動器 （FDHOST 啟動器） 服務[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]全文檢索搜尋啟動篩選背景程式主機處理序，以便處理全文檢索搜尋篩選和斷詞。 若要使用全文檢索搜尋，您必須執行這個服務。 FDHOST 啟動器服務是一個與特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體有關的執行個體感知服務。 FDHOST 啟動器服務會將服務帳戶資訊傳播至啟動的每個篩選背景程式主機處理序。 如需篩選背景程式主機處理序的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜全文檢索搜尋架構＞。  
  
  
