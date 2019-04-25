---
title: 從 Analysis Services 中的 Power Pivot 還原 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 75290c6b877c3bb10cd42fbb10f1c087310791d3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472248"
---
# <a name="restore-from-power-pivot"></a>從 PowerPivot 還原
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  您可以在 SQL Server Management Studio 中使用 [從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 還原] 功能，於 Analysis Services 執行個體上建立新的表格式模型資料庫 (以表格式模式執行)，或是從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿 (.xlsx) 還原到現有的資料庫。  
  
> [!NOTE]  
>  SQL Server Data Tools 中的 [從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 匯入] 專案範本提供了類似的功能。 如需詳細資訊，請參閱 <<c0> [ 從 Power Pivot 匯入](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)。  
  
 使用 [從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]還原] 功能時，請牢記以下事項：  
  
-   若要使用 [從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]還原] 功能，您必須以 Analysis Services 執行個體上伺服器管理員角色的成員身分登入。  
  
-   Analysis Services 執行個體服務帳戶必須對您要從中還原的活頁簿檔案具有讀取權限。  
  
-   依預設，當您從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]還原資料庫時，表格式模型資料庫的 [資料來源模擬資訊] 屬性會設為 [預設值]，而這是指定 Analysis Services 執行個體服務帳戶。 建議您在 [資料庫屬性] 中，將模擬認證變更為 Windows 使用者帳戶。 如需詳細資訊，請參閱 <<c0> [ 模擬](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)。  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料模型中的資料將會複製到 Analysis Services 執行個體上現有或新的表格式模型資料庫。 如果您的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿包含連結資料表，這些資料表將會重新建立成為不具資料來源的資料表，類似於使用 [貼上至新資料表] 所建立的資料表。  
  
### <a name="to-restore-from-power-pivot"></a>從 PowerPivot 還原  
  
1.  在 SSMS 中，針對您要還原至其上的 Active Directory 執行個體，以滑鼠右鍵按一下 [資料庫]，然後按一下 [從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 還原]。  
  
2.  在 [從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 還原] 對話方塊的 [還原來源] 中，按一下 [備份檔案] 中的 [瀏覽]，然後選取要從中還原的 .abf 或 .xslx 檔案。  
  
3.  在 [還原目標] 的 [還原資料庫] 中，輸入新資料庫或現有資料庫的名稱。 如果您沒有指定名稱，就會使用活頁簿的名稱。  
  
4.  按一下 [儲存位置] 中的 [瀏覽]，然後選取要儲存資料庫的位置。  
  
5.  在 [選項] 中，保持核取 [包含安全性資訊]。 從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿還原時，這項設定並不適用。  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型資料庫](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)   
 [從 Power Pivot 匯入](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)  
  
  
