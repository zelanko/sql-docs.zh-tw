---
title: 開啟、檢視及列印死結檔案 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], printing files
- deadlocks [SQL Server], opening files
- opening deadlock files
- printing deadlock files
ms.assetid: 5061b13f-2cb7-457a-b8d0-fbd437b510ab
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 08bacd7a99e45e10163216c69057b167088441ad
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063913"
---
# <a name="open-view-and-print-a-deadlock-file-sql-server-management-studio"></a>開啟、檢視及列印死結檔案 (SQL Server Management Studio)
  當 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 產生死結時，您可以擷取死結資訊並將資訊儲存至檔案。 在儲存死結檔案之後，您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中開啟檔案，再檢視或列印它。  
  
### <a name="to-open-and-view-a-deadlock-file"></a>若要開啟和檢視死結檔案  
  
1.  **在的 [檔案**] 功能表上 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，指向 [**開啟**]， **File**然後按一下 [檔案]。  
  
2.  在 [開啟檔案]  對話方塊中，從 [檔案類型]  方塊中選取 .xdl 檔案類型。 您現在會有一份只有死結檔案的篩選清單。  
  
### <a name="to-print-a-deadlock-file"></a>若要列印死結檔案  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的 [檔案]**** 功能表上，指向 [開啟]**** 並按一下 [檔案]****。  
  
2.  在 [開啟檔案]  對話方塊中，從 [檔案類型]  方塊中選取 .xdl 檔案類型。 您現在會有一份只有死結檔案的篩選清單。  
  
3.  選取您要列印的死結檔案，並按一下 [開啟]****。  
  
4.  在 [檔案]**** 功能表上，按一下 [列印]****。  
  
## <a name="see-also"></a>另請參閱  
 [儲存鎖死圖形 &#40;SQL Server Profiler&#41;](save-deadlock-graphs-sql-server-profiler.md)  
  
  
