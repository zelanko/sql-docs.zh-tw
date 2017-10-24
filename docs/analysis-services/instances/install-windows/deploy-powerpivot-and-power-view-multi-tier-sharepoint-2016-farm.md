---
title: "部署 PowerPivot 和 Power View 的多層 SharePoint 2016 伺服器陣列 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e36a632-0750-4247-92b6-1fe38c7a4ce2
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d7dc4fc8e7b1926359096447183dc17c9c1a1cd8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="deploy-powerpivot-and-power-view---multi-tier-sharepoint-2016-farm"></a>部署 PowerPivot 和 Power View 的多層 SharePoint 2016 伺服器陣列
  **摘要︰** 這份技術白皮書提供 SharePoint 系統管理員和架構設計人員有關下列作業的詳細逐步指示：在具有多部伺服器的 SharePoint 伺服器陣列中部署和設定 Microsoft BI 示範環境 (根據 SharePoint Server 2016 的預覽版本、Office Online Server 以及 SharePoint 2016 的 SQL Server 2016 BI 堆疊)。 在簡單介紹重要架構變更和對應系統相依性之後，同時概述軟體和組態需求，以及建議的部署路徑來透過三個主要階段啟用和驗證 BI 功能。 這份技術白皮書也會討論 SharePoint Server 2016 Beta 2、Office Online Server Preview 和 SQL Server 2016 CTP 3.1 版本中的已知問題，以及建議適當的因應措施。 最終產品版本將不再需要這些因應措施。 部署 RTM 版本時，請檢查這份白皮書的更新版本。  
  
 **作者：**Kay Unkroth, Jason Haak  
  
 **技術校閱：** Adam Saxton、Anne Zorner、Craig Guyer、Frank Weigel、Gregory Appel、Heidi Steen、Kasper de Jonge、Kirk Stark、Klaus Sobel、Mike Plumley、Mike Taghizadeh、Patrick Wheeler、Riccardo Muti、Steve Hord  
  
 **發行時間：**2016 年 1 月  
  
 **適用於︰** SQL Server 2016 CTP3.1、SharePoint 2016 Preview、Office Online Server Preview  
  
 若要檢閱文件，請下載 Word 文件： [Deploying SQL Server 2016 PowerPivot and Power View in a Multi-Tier SharePoint 2016 Farm](http://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Deploying%20SQL%20Server%202016%20PowerPivot%20and%20Power%20View%20in%20a%20Multi-Tier%20SharePoint%202016%20Farm.docx) (在多層 SharePoint 2016 伺服器陣列中部署 SQL Server 2016 PowerPivot 和 Power View)。  
  
  

