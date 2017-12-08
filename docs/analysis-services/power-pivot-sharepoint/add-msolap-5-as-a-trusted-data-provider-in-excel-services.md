---
title: "加入 MSOLAP.5 做為 Excel Services 中的受信任的資料提供者 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c1f40fa4-de6d-41ee-8124-14b4d65988f5
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 64b3ea1f946e73a3f56cd70b5e88d9752d74a238
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>加入 MSOLAP.5 做為 Excel Services 中受信任的資料提供者
  MSOLAP.5 是指 Analysis Services OLE DB Provider for SQL Server 2012。 Excel Services 必須信任此提供者，才能提出連接要求，在伺服器上產生 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料。  
  
 如果您使用 [ [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具] 設定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，MSOLAP.5 可能已經是受信任的提供者，因為工具包含符合此需求的動作。 不過，如果您使用 PowerShell、管理中心，或在組態工具中排除受信任的提供者動作，可能會遺失提供者，在此情況下，您應該趁設定伺服器陣列時立即將其加入，以進行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料存取。  
  
 只需要為每個 Excel Services 服務應用程式執行此步驟一次。  
  
 電腦上必須已安裝 OLE DB 提供者， [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 伺服器或 Excel Services 伺服器等實體伺服器才能處理 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料要求。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安裝一律包含 OLE DB 提供者，但是如果在沒有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的電腦上執行 Excel Services，您必須手動安裝此提供者。 如需詳細資訊，請參閱 [在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859)。  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>將受信任的提供者加入至 Excel Services  
  
1.  在 [管理中心]，按一下 **[管理服務應用程式]**，然後按一下 Excel Services 服務應用程式。  
  
2.  按一下 **[信任的資料提供者]**。  
  
3.  確認 MSOLAP.5 出現在清單中。 根據您設定 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的方式，MSOLAP.5 可能已經是受信任的提供者。  
  
4.  如果未列出，請按一下 **[新增信任的資料提供者]**。  
  
5.  在 [提供者識別碼] 中，輸入 **MSOLAP.5**。  
  
6.  對於 [提供者類型]，請確認已選取 OLE DB。  
  
7.  在 [提供者描述] 中，輸入 **Microsoft OLE DB Provider for OLAP Services 11.0**。  
  
  
