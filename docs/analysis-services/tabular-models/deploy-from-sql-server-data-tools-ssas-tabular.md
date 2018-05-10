---
title: 從 SQL Server Data Tools 部署 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d9bc5b48a7691bb4fbde4c8f7298325103950b02
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2018
---
# <a name="deploy-from-sql-server-data-tools"></a>從 SQL Server 資料工具部署
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  使用本主題中的工作，若要使用 [部署] 命令在 SSDT 中部署表格式模型方案。  
  
##  <a name="bkmk_deploy"></a> 設定部署選項與部署伺服器屬性  
 在您部署表格式模型方案之前，必須先指定 [部署選項] 與 [部署伺服器] 屬性。 如需部署屬性和設定的詳細資訊，請參閱[表格式模型方案部署](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)。  
  
#### <a name="to-configure-options-and-properties"></a>若要設定選項和屬性  
  
1.  在 SSDT 中，在**方案總管 中**，以滑鼠右鍵按一下專案名稱，然後按**屬性**。  
  
2.  在**\<專案名稱 > 屬性**對話方塊，請在**部署選項**，指定屬性設定，如果不同於預設設定。  
  
    > [!NOTE]  
    >  快取模式之模型的 [查詢模式] 一律是 [記憶體內部]。  
  
    > [!NOTE]  
    >  您無法在 DirectQuery 模式下指定模型的 [模擬設定]。  
  
3.  在 [部署伺服器] 中，指定 [伺服器] \(名稱)、[版本]、[資料庫] \(名稱) 及 [Cube 名稱] 屬性設定 (如果與預設設定不同)，然後按一下 [確定]。  
  
> [!NOTE]  
>  您也可以指定 [預設部署伺服器] 屬性設定，自動將您建立的任何新專案部署至指定的伺服器。 如需詳細資訊，請參閱[設定預設資料模型和部署屬性](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)。  
  
##  <a name="bkmk_deploy_proc"></a> 部署表格式模型  
  
#### <a name="to-deploy-a-tabular-model"></a>若要部署表格式模型
  
-   在 SSDT 中，在**建置**功能表上，按一下 **部署\<專案名稱 >**。  
  
     [部署] 對話方塊將會出現，並指出模型中包含之每個資料表的中繼資料部署與處理狀態 (除非 [處理選項] 屬性設為 [不處理])。 完成部署程序之後，使用 SSMS 連接到 Analysis Services 執行個體，並確認已建立新的模型資料庫物件，或使用用戶端報表應用程式連接到已部署的模型。  
  
##  <a name="bkmk_deploy_status"></a> 部署狀態  
 [部署] 對話方塊可讓您監視部署作業的進度。 您也可以停止部署作業。  
  
 **狀態**  
 指出部署作業是否成功。  
  
 **詳細資料**  
 列出已部署的中繼資料項目、每個中繼資料項目的狀態，並提供每個問題的訊息。  
  
 **停止部署**  
 按一下可停止部署作業。 如果部署作業耗費時間過長，或者如果有太多錯誤，這個選項會很有用。  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型方案部署](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)   
 [設定預設的資料模型和部署屬性](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
  
  
