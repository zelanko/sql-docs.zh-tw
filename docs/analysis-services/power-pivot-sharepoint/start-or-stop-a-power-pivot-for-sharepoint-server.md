---
title: 啟動或停止 Power Pivot for SharePoint 伺服器 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c581135e13811e82535fa7735f1116f413d6752
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="start-or-stop-a-power-pivot-for-sharepoint-server"></a>啟動或停止 Power Pivot for SharePoint Server
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務和 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 執行個體會在相同的本機應用程式伺服器上一起運作，以支援 SharePoint 伺服陣列中協調的要求和資料處理。  
  
 本主題包含下列幾節：  
  
 [服務相依性](#dependencies)  
  
 [啟動或停止服務](#startstop)  
  
 [停止 PowerPivot 伺服器的影響](#effects)  
  
##  <a name="dependencies"></a> 服務相依性  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務與隨其一起安裝在相同實體伺服器上的本機 Analysis Services 伺服器執行個體具有相依性。 如果您停止 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務，也必須手動停止本機 Analysis Services 伺服器執行個體。 如果某項服務正在執行，但另一項服務並未執行，將會發生 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料處理的要求配置錯誤。  
  
 只有當您要診斷或疑難排解問題時，Analysis Services 伺服器才應該獨自執行。 但是在其他情況下，此伺服器則需要在相同的伺服器上以本機執行的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務。  
  
##  <a name="startstop"></a> 啟動或停止服務  
 請務必使用管理中心來啟動或停止 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務或 Analysis Services 伺服器執行個體。 管理中心可讓您從相同的頁面一起啟動或停止服務。 此外，管理中心也會使用稱為 **一個或多個服務已經啟動或停止** 的計時器工作，以重新啟動它認為應該執行的服務。 如果您使用非 SharePoint 工具停止 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務或 Analysis Services，此服務會在計時器工作執行時重新啟動。  
  
 啟動和停止服務是套用至實體服務執行個體的動作。 如果伺服陣列中有其他 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 伺服器，在伺服陣列中的其他伺服器會繼續接受 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的要求。  
  
 您無法同時啟動或停止在伺服陣列的所有實體服務。 您必須選取每部伺服器，然後啟動或停止特定服務。  
  
 您無法啟動、暫停或停止特定 Web 應用程式的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務，但是您可以從預設連線清單移除服務，使其無法使用。 如需詳細資訊，請參閱[在管理中心將 Power Pivot 服務應用程式連接到 SharePoint Web 應用程式](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)。  
  
1.  在管理中心的 [系統設定] 中，按一下 [管理伺服器上的服務]。  
  
2.  在 [伺服器] 頁面的頂端，按一下向下箭頭，然後按一下 [變更伺服器]。  
  
3.  選取具有您要啟動或停止的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務或 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 執行個體的 SharePoint 伺服器。  
  
4.  選取服務，然後按一下動作。 請記得要以成對的方式啟動或停止服務。 如果您啟動或停止 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務，請務必也啟動或停止在相同電腦上執行的 Analysis Services 伺服器執行個體。  
  
##  <a name="effects"></a> 停止 PowerPivot 伺服器的影響  
 下表描述在 SharePoint 伺服器上停止 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務及 Analysis Services 服務的影響。  
  
|影響的項目|Description|  
|---------------|-----------------|  
|現有的查詢|在 Analysis Services 伺服器上進行中的查詢將會立即停止。 使用者將會收到找不到資料或找不到資料來源連接的錯誤。|  
|目前正在處理的現有資料重新整理工作|在目前的 Analysis Services 伺服器上進行中的作業將會立即停止。 資料重新整理將會失敗，而且會將錯誤記錄至資料重新整理記錄。<br /><br /> 在您使用 [SharePoint 管理中心] 中的 [檢查工作狀態] 頁面停止服務之前，您可以檢視目前工作的狀態。<br /><br /> 雖然要知道哪些作業目前正在處理是可能的，但是並沒有任何方法可檢視佇列本身是否有其他作業即將開始。|  
|佇列中現有的資料重新整理要求|已排程的資料重新整理要求，仍然會在處理佇列中，以等待排程的完整循環 (也就是在下一個開始時間之前，它會一直待在佇列中)。 如果到時仍未重新啟動 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務，則會卸除資料重新整理要求並記錄錯誤。|  
|對於查詢或資料重新整理的新要求|如果您停止伺服陣列中唯一的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 伺服器，將不會處理對 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的新要求，而且對於資料的要求將會導致找不到資料的錯誤。<br /><br /> 如果您有額外的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 伺服器，要求將會移至其中一個可用的伺服器。|  
|使用量資料|停止服務時將不會收集使用量資料。|  
  
## <a name="see-also"></a>另請參閱  
 [設定 Power Pivot 服務帳戶](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)  
  
  
