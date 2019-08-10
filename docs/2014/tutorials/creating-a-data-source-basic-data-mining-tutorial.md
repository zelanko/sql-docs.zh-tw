---
title: 建立資料來源 (基本資料採礦教學課程) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d7107c32-69ed-49a8-9b6e-32753eebf42c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7fc2d6eebc342de7126ebd3c8c41c12e07107089
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68888745"
---
# <a name="creating-a-data-source-basic-data-mining-tutorial"></a>建立資料來源 (基本資料採礦教學課程)
  *資料來源*是在您的專案中儲存和管理的資料連線, 並部署至您[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的資料庫。 資料來源包含來源資料所在的伺服器和資料庫名稱，以及任何其他必要的連接屬性。  
  
> [!IMPORTANT]  
>  資料庫的名稱為 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]。 如果您尚未安裝此資料庫, 請參閱[MICROSOFT SQL 範例資料庫](https://go.microsoft.com/fwlink/?LinkId=88417)頁面。  
  
### <a name="to-create-a-data-source"></a>建立資料來源  
  
1.  在**方案總管**中, 以滑鼠右鍵按一下 [**資料來源**] 資料夾, 然後選取 [**新增資料來源**]。  
  
2.  在 [**歡迎使用資料來源嚮導]** 頁面上, 按 **[下一步]** 。  
  
3.  在 [**選取如何定義連接**] 頁面上, 按一下 [**新增**], 將[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]連接加入資料庫。  
  
4.  在 [**連線管理員**] 的 [**提供者**] 清單中, 選取 [**原生 OLE DB\SQL Server native Client 11.0**]。  
  
5.  在 [**伺服器名稱**] 方塊中, 輸入或選取您已安裝[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]的伺服器名稱。  
  
     例如, 如果資料庫裝載于本機伺服器上, 請輸入**localhost** 。  
  
6.  在 [**登入伺服器**] 群組中, 選取 [**使用 Windows 驗證**]。  
  
    > [!IMPORTANT]  
    >  實作者應該盡可能使用 Windows 驗證，因為它所提供的驗證方法要比 SQL Server 驗證更安全。 但是，提供 SQL Server 驗證的目的是為了回溯相容性。 如需驗證方法的詳細資訊, 請參閱[資料庫引擎設定-帳戶提供](../../2014/sql-server/install/database-engine-configuration-account-provisioning.md)。  
  
7.  在 [**選取或輸入資料庫名稱**] 清單中, [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]選取 [], 然後按一下 **[確定]** 。  
  
8.  按一下 [下一步]。  
  
9. 在 [模擬**資訊**] 頁面上, 按一下 [**使用服務帳戶**], 然後按 **[下一步]** 。  
  
     在 [**正在完成嚮導]** 頁面上, 請注意, 根據預設, 資料來源的名稱為 [艾德作品] [DW 2012]。  
  
10. 按一下 [ **完成**]。  
  
     新的資料來源 [艾德公司 DW 2012] 會出現在方案總管的 [**資料來源**] 資料夾中。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [建立資料來源視圖&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/creating-a-data-source-view-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>本課程的前一項工作  
 [建立 Analysis Services 專案&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [建立資料來源 &#40;SSAS 多維度&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional)   
 [定義資料來源](https://docs.microsoft.com/analysis-services/lesson-1-2-defining-a-data-source)   
 [設定模擬選項 &#40;SSAS - 多維度&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional)  
  
  
