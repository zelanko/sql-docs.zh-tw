---
title: 記錄清除工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.historycleanuptask.f1
helpviewer_keywords:
- history tables [SQL Server]
- History Cleanup task [Integration Services]
ms.assetid: 5defc5b9-dfd3-4859-a7fe-ac8c2b5480f8
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d9866ea65bdd4f7fdb9e867898c4ae85a0c0f189
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271654"
---
# <a name="history-cleanup-task"></a>記錄清除工作
  「記錄清除」工作會刪除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 資料庫中下列記錄資料表的項目。  
  
-   backupfile  
  
-   backupfilegroup  
  
-   backupmediafamily  
  
-   backupmediaset  
  
-   backupset  
  
-   restorefile  
  
-   restorefilegroup  
  
-   restorehistory  
  
 藉由使用「記錄清除」工作，封裝便能刪除關於備份和還原活動、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，以及資料庫維護計畫的記錄資料。  
  
 這項工作會封裝 sp_delete_backuphistory 系統預存程序，並將指定的日期傳遞至該程序做為引數。 如需詳細資訊，請參閱 [sp_delete_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql)。  
  
## <a name="configuration-of-the-history-cleanup-task"></a>設定記錄清除工作  
 這項工作包含指定歷程記錄資料表中最舊日期之資料的屬性。 您可以用目前日期起算的天數、週數、月數或年數表示該日期，而工作會自動將間隔翻譯成日期。  
  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」設定屬性 這項工作位於「 **設計師」中** [工具箱] **的** [維護計畫工作] [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 區段。  
  
 如需有關可在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [記錄清除工作 &#40;維護計畫&#41;](../../relational-databases/maintenance-plans/history-cleanup-task-maintenance-plan.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](integration-services-tasks.md)   
 [控制流程](control-flow.md)  
  
  
