---
title: 作業屬性 (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.reportserver.jobproperties.f1
ms.assetid: 807ffd0e-9363-4f8f-9c36-c5d746ad19fd
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 0c4beffc83f4e766780705662706d65b51a0c945
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036949"
---
# <a name="job-properties-management-studio"></a>作業屬性 (Management Studio)
  您可以使用 [作業屬性] 頁面來檢視有關進行中報表或訂閱的資訊，然後再加以取消。  
  
 若要開啟此頁面，請啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、連線至報表伺服器，然後開啟 [作業] 資料夾。 以滑鼠右鍵按一下執行中的作業，然後按一下 [屬性]。  
  
> [!NOTE]  
>  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services 不支援這項功能。 因此，當您執行 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]時，不會出現此頁面。  
  
## <a name="tasks"></a>工作  
 在您檢視有關某項作業的資訊之前，請重新整理此頁面，以便擷取報表伺服器上目前正在執行之作業的相關資訊：  
  
1.  開啟報表伺服器資料夾。  
  
2.  以滑鼠右鍵按一下 [作業]，然後按一下 [重新整理]。  
  
3.  如果已列出作業，請以滑鼠右鍵按一下該作業，然後按一下 [屬性]。  
  
## <a name="options"></a>選項。  
 **作業識別碼**  
 在處理作業時指派給作業的 GUID。 此值是在每次報表或訂閱執行時隨機產生的。  
  
 **作業狀態**  
 有效值為 **[新增]** 和 **[正在執行]**。 當作業啟動時，狀態永遠是 **[新增]** 。 60 秒之後，狀態會變更為 **[正在執行]**。 您必須重新整理此頁面，才能收取變更。  
  
 **作業類型**  
 有效值為 [使用者] 和 [系統]。 使用者作業是由個別使用者起始的任何作業。 這種作業包括視需要執行報表、手動產生報表記錄快照集，或者手動建立報表執行快照集。 進行中標準訂閱也是使用者作業。 系統作業是由報表伺服器起始的作業。 系統作業包括由排程觸發的報表處理。  
  
 **作業動作**  
 若為報表，此資料行會顯示執行中的報表執行處理序。 這個值永遠是 [轉譯]。  
  
 **作業描述**  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 預設不會提供作業描述。  
  
 **伺服器名稱**  
 顯示正在處理此作業之報表伺服器的名稱。 如果您設定了向外延展部署，這個值將會顯示正在處理此作業的伺服器。  
  
 **報表名稱**  
 顯示報表的名稱。 依據描述來識別訂閱。  
  
 **報表路徑**  
 顯示報表伺服器資料夾階層中之報表的路徑。  
  
 **Start Time**  
 顯示處理序的開始時間。  
  
 **使用者名稱**  
 若為使用者起始的處理序，此資料行會顯示使用者的名稱。 若為系統作業，這就是報表伺服器的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [Management Studio F1 說明中的報表伺服器](report-server-in-management-studio-f1-help.md)   
 [連接至 Management Studio 中的報表伺服器](connect-to-a-report-server-in-management-studio.md)   
 [管理執行中的處理序](../subscriptions/manage-a-running-process.md)  
  
  