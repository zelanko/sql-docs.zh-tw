---
title: 部署 PowerPivot 和 Power View-多層式 SharePoint 2016 伺服器陣列 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ee295f354de5479f5af8add49cb7aee2985a687f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63054575"
---
# <a name="deploy-powerpivot-and-power-view---multi-tier-sharepoint-2016-farm"></a>部署 PowerPivot 和 Power View-多層式 SharePoint 2016 伺服器陣列
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  **摘要：** 摘要：這份白皮書提供 SharePoint 系統管理員和架構設計人員的詳細逐步指示部署和設定 Microsoft BI 示範環境中以 SharePoint 伺服器的 Preview 版本為基礎的多個伺服器的 SharePoint 伺服器陣列2016 年 office Online Server 以及 SQL Server 2016 BI 堆疊 SharePoint 2016。 在簡單介紹重要架構變更和對應系統相依性之後，同時概述軟體和組態需求，以及建議的部署路徑來透過三個主要階段啟用和驗證 BI 功能。 這份技術白皮書也會討論 SharePoint Server 2016 Beta 2、Office Online Server Preview 和 SQL Server 2016 CTP 3.1 版本中的已知問題，以及建議適當的因應措施。 最終產品版本將不再需要這些因應措施。 部署 RTM 版本時，請檢查這份白皮書的更新版本。  
  
 **作者：** Kay Unkroth, Jason Haak  
  
 **技術校閱：** Adam Saxton、 Anne Zorner、 Craig Guyer、 Frank Weigel、 Gregory Appel、 Heidi Steen、 Kasper de Jonge、 Kirk Stark、 Klaus Sobel、 Mike Plumley、 Mike Taghizadeh、 Patrick Wheeler、 Riccardo Muti、 Steve Hord  
  
 **發行時間：** 2016 年 1 月  
  
 **適用於：** SQL Server 2016 CTP3.1、SHAREPOINT 2016 Preview、 Office Online Server Preview  
  
 若要檢閱文件，請下載 Word 文件： [Deploying SQL Server 2016 PowerPivot and Power View in a Multi-Tier SharePoint 2016 Farm](http://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Deploying%20SQL%20Server%202016%20PowerPivot%20and%20Power%20View%20in%20a%20Multi-Tier%20SharePoint%202016%20Farm.docx) (在多層 SharePoint 2016 伺服器陣列中部署 SQL Server 2016 PowerPivot 和 Power View)。  
  
  
