---
title: "維護清除工作 (維護計畫) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.maint.cleanup.f1
helpviewer_keywords: Maintenance Cleanup Task dialog box
ms.assetid: 022b679c-6799-4c13-9185-814224a20412
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3934b29a7067cda0cd74656c2f6fa38f0748e658
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="maintenance-cleanup-task-maintenance-plan"></a>維護清除工作 (維護計畫)
  使用 **[維護清除工作]** ，即可移除與維護計畫相關的舊檔案 (包括維護計畫和資料庫備份檔案所建立的文字報表)。  
  
> [!NOTE]  
>  維護清除工作不會自動刪除所指定目錄之子資料夾中的檔案。 這項功能可降低利用「維護清除」工作刪除檔案這類惡意攻擊的可能性。 如果您要刪除第一層子資料夾中的檔案，必須選取 [包含第一層的子資料夾]。  
  
## <a name="options"></a>選項。  
 **連接**  
 顯示目前的連接。  
  
 **新增**  
 建立新的伺服器連接，以便執行此工作時使用。 下面會描述 **[新增連接]** 對話方塊。  
  
 **備份檔案**  
 刪除備份檔案。  
  
 **維護計畫文字報表**  
 刪除先前執行之維護計畫的文字報表。  
  
 **刪除特定檔案**  
 刪除 [檔案名稱] 方塊中提供的特定檔案。  
  
 **檔案名稱**  
 要刪除的檔案路徑與名稱。  
  
 **根據副檔名搜尋資料夾並刪除檔案**  
 刪除指定之資料夾中具有指定之副檔名的所有檔案。 使用此方法即可同時刪除多個檔案，例如 Tuesday 資料夾中副檔名為 .bak 的所有備份檔案。  
  
 **資料夾**  
 包含要刪除檔案的資料夾路徑與名稱。  
  
 **副檔名**  
 提供要刪除的檔案副檔名。  
  
 **包含第一層的子資料夾**  
 從 [資料夾] 底下的第一層子資料夾中，刪除具有 [副檔名] 中所指定之副檔名的檔案。  
  
 **在工作執行階段依據檔案存在時間刪除檔案**  
 在 [刪除早於下列時限的檔案] 方塊中提供數字以及時間單位，以指定您要刪除之檔案的最低存在時間。  
  
 **刪除早於下列時限的檔案**  
 提供數字以及時間單位 (日、週、月或年)，以指定您要刪除之檔案的最低存在時間。 存在時間超過指定時間的檔案會遭到刪除。  
  
 **檢視 T-SQL**  
 根據選取的選項，檢視此工作在伺服器上執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
> [!NOTE]  
>  受影響的物件數目較為大量時，會多花一些時間才會顯示。  
  
## <a name="new-connection-dialog-box"></a>新增連接對話方塊  
 **連接名稱**  
 輸入新連接的名稱。  
  
 **選取或輸入伺服器名稱**  
 選取執行此工作時要連接的伺服器。  
  
 **…**  
 選取此項以檢視可用伺服器的清單。  
  
 **輸入要登入到伺服器的資訊**  
 指定如何對伺服器進行驗證。  
  
 **使用 Windows 整合式安全性**  
 使用 Microsoft Windows 驗證來連接 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體。  
  
 **使用特定的使用者名稱和密碼**  
 使用 SQL Server 驗證來連接 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體。 無法使用此選項。  
  
 **使用者名稱**  
 提供驗證時要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 無法使用此選項。  
  
 **密碼**  
 提供驗證時要使用的密碼。 無法使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [維護計畫](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  
