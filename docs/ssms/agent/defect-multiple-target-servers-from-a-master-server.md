---
title: "使多個目標伺服器脫離主要伺服器 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
- multiple target server defections
ms.assetid: 61a3713b-403a-4806-bfc4-66db72ca1156
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d24f986e0274592b8984c9bf5d493261781b8f77
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="defect-multiple-target-servers-from-a-master-server"></a>使多個目標伺服器脫離主要伺服器
本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]的多伺服器管理組態中脫離多個目標伺服器。 從主要伺服器執行這個程序。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-defect-multiple-target-servers-from-a-master-server"></a>若要使多個目標伺服器脫離主要伺服器  
  
1.  在 **[物件總管]**中，展開設定為主要伺服器的伺服器。  
  
2.  在 [SQL Server Agent]，再指向 [多伺服器管理]，然後按一下 [管理目標伺服器]。  
  
3.  按一下 **[公佈指示]**，然後在 **[指示類型]** 清單中選取 **[脫離]**。  
  
4.  在 **[收件者]**下，執行下列其中一項：  
  
    -   按一下 **[所有目標伺服器]** ，脫離此主要伺服器的所有目標伺服器。 如果您要完整解除安裝目前的多伺服器管理組態，請使用此選項。  
  
    -   按一下 **[下列目標伺服器]**，然後按一下對應的 **[選取]** 方塊，脫離此主要伺服器的部份目標伺服器，但不是所有目標伺服器。  
  
## <a name="see-also"></a>另請參閱  
[建立多伺服器環境](../../ssms/agent/create-a-multiserver-environment.md)  
[將整個企業的管理自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[Defect a Target Server from a Master Server](../../ssms/agent/defect-a-target-server-from-a-master-server.md)  
  

