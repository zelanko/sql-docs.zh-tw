---
title: 檢視或修改作業 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- jobs [SQL Server Agent], viewing
- modifying jobs
- viewing jobs
- SQL Server Agent jobs, viewing
- SQL Server Agent jobs, modifying
- displaying jobs
ms.assetid: 57f649b8-190c-4304-abd7-7ca5297deab7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 87e5644329742712e112fd3df97f601838f7faea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63245516"
---
# <a name="view-or-modify-jobs"></a>檢視或修改作業
  您可檢視您所建立的任何作業。 在執行作業之後，您也可以檢視其記錄。 檢視作業的記錄可讓您了解作業執行的時間、整體作業的狀態，以及作業中每個作業步驟的狀態。 您可以了解作業過去是否曾經失敗、作業最後一次順利完成的時間，以及作業每次執行時所建立的輸出。 無論擁有者是誰， **系統管理員** 固定伺服器角色的成員一律可以檢視或修改作業。  
  
> [!NOTE]  
>  作業至少必須已經執行過一次才會有作業記錄。 您可以限制作業記錄的總大小與其中每個作業所佔的大小。  
  
 最後，您可以修改作業以符合新的需求。 您可以修改：  
  
-   回應選項  
  
-   排程  
  
-   作業步驟  
  
-   擁有權  
  
-   作業類別目錄  
  
-   目標伺服器 (只適用多伺服器作業)  
  
 若要確定對多重伺服器作業所做的變更會生效，您必須將變更發佈到下載清單，目標伺服器才能下載更新的作業。 若要確保目標伺服器具有目前最新的作業定義，請在更新該多重伺服器作業後發佈一個 INSERT 指示，如下所示：  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
 如需詳細資訊，請參閱[sp_purge_jobhistory &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql)。  
  
 
  **系統管理員** 固定伺服器角色的成員不僅可以檢視所有作業的定義或記錄，也可修改任何作業。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|說明如何檢視 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業。|[檢視作業](view-a-job.md)|  
|說明如何檢視 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業的歷程記錄。|[檢視作業記錄](view-the-job-history.md)|  
|說明如何刪除 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業的歷程記錄內容。|[清除作業歷程記錄](clear-the-job-history-log.md)|  
|說明如何設定 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業的記錄大小限制。|[調整作業記錄大小](resize-the-job-history-log.md)|  
|說明如何變更 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業的屬性。|[Modify a Job](modify-a-job.md)|  
  
## <a name="see-also"></a>另請參閱  
 [sysjobhistory &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysjobhistory-transact-sql)  
  
  
