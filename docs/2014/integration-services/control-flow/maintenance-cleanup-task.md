---
title: 維護清除工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.maintenancecleanuptask.f1
helpviewer_keywords:
- deleting files
- removing files
- Maintenance Cleanup task
ms.assetid: 73ad3cd6-9a6d-44cf-905f-c56aa658bf42
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 90ef3f848df9bd9b0e321e96ad558d4ed452f21a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112228"
---
# <a name="maintenance-cleanup-task"></a>維護清除工作
  「維護清除」工作會移除與維護計畫相關的檔案，包括資料庫備份檔案以及維護計畫所建立的報表。 如需詳細資訊，請參閱 [維護計畫](../../relational-databases/maintenance-plans/maintenance-plans.md) 和 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。  
  
 封裝可以使用「維護清除」工作來移除指定伺服器上的備份檔案或維護計畫報表。 「維護清除」工作包含一個選項，可用來移除某個特定檔案或移除資料夾中的某個檔案群組。 您也可以選擇指定要刪除之檔案的副檔名。  
  
 當您設定「維護清除」工作來移除備份檔時，預設副檔名是 BAK。 如果是報表檔案，預設副檔名是 TXT。 您可以更新副檔名，以符合您的需求，唯一的限制是副檔名的長度必須小於 256 個字元。  
  
 通常您會想移除已經不需要的舊檔案，而且可以設定「維護清除」工作，以刪除已經到達指定存在時間的檔案。 例如，您可以設定工作以刪除存在時間已超過四週的檔案。 您可以使用天數、週數、月數或年數來指定要刪除之檔案的存在時間。 如果沒有指定要刪除之檔案的最低存在時間，則會刪除指定類型的所有檔案。  
  
 與舊版的「維護清除」工作不同， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版的工作並不會自動刪除指定目錄之子目錄中的檔案。 此條件約束會縮小任何可能利用「維護清除」工作功能惡意刪除檔案之攻擊的介面區。 若要刪除第一層子資料夾，您必須選取 [維護清除工作] 對話方塊中的 [包含第一層的子資料夾] 選項，明確選擇要執行此動作。  
  
## <a name="configuration-of-the-maintenance-cleanup-task"></a>設定維護清除工作  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」設定屬性 這項工作位於「 **設計師」中** [工具箱] **的** [維護計畫工作] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 區段。  
  
 如需有關可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [維護清除工作 &#40;維護計畫&#41;](../../relational-databases/maintenance-plans/maintenance-cleanup-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具中設定這些屬性的詳細資訊，請參閱 [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](integration-services-tasks.md)   
 [控制流程](control-flow.md)  
  
  
