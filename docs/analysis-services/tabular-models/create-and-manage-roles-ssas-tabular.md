---
title: 建立及管理角色 |Microsoft 文件
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.bidtoolset.rolemanager.f1
- sql13.asvs.bidtoolset.roledb.f1
ms.assetid: e23d27a8-e968-4082-9dbe-963fc724b5d9
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 788e0cab02a0b3931c0c8a702989366983e33b65
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-manage-roles"></a>建立及管理角色 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  表格式模型中的角色定義模型的成員權限。 您可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的 [角色管理員] 對話方塊來定義模型專案的角色。 部署模型之後，資料庫管理員即可使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]管理角色。  
  
 這篇文章中的工作描述如何建立及管理角色使用角色管理員 對話方塊中的模型撰寫期間[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 管理已部署的模型資料庫中角色的相關資訊，請參閱[表格式模型角色](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md)。  
  
## <a name="tasks"></a>工作  
 若要建立、編輯、複製及刪除角色，您要使用 [角色管理員] 對話方塊。 若要檢視 [角色管理員] 對話方塊，請在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中按一下 [模型] 功能表，然後按一下 [角色管理員]。  
  
###  <a name="bkmk_new_role"></a> 若要建立新角色  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，按一下 [模型] 功能表，然後按一下 [角色管理員]。  
  
2.  在 [角色管理員] 對話方塊中，按一下 [新增]。  
  
     反白顯示的新角色即會加入至 [角色] 清單中。  
  
3.  在 [角色] 清單的 [名稱] 欄位中，輸入角色的名稱。  
  
     依預設，每個新角色的預設角色名稱是以累加的方式進行編號。 建議您輸入清楚識別成員類型的名稱，例如「財務經理」或「人力資源專員」。  
  
4.  在 [權限] 欄位中，按一下向下箭頭，然後選取下列其中一個權限類型：  
  
    |權限|Description|  
    |----------------|-----------------|  
    |**無**|成員無法對模型結構描述進行任何修改，也無法查詢資料。|  
    |**讀取**|成員可以查詢資料 (根據資料列篩選)，但無法對模型結構描述進行任何變更。|  
    |**讀取和處理**|成員可以查詢資料 (根據資料列層級篩選) 並執行「處理」和「全部處理」作業，但無法對模型結構描述進行任何變更。|  
    |**處理**|成員可以執行「處理」和「全部處理」作業。 無法修改模型結構描述，也無法查詢資料。|  
    |**系統管理員**|成員可以對模型結構描述進行修改，也可以查詢所有資料。|  
  
5.  若要輸入角色的描述，請按一下 [描述] 欄位，然後輸入描述。  
  
6.  如果您建立的角色具有「讀取」或「讀取和處理」權限，您可以使用 DAX 公式加入資料列篩選。 若要加入資料列篩選，請按一下 [資料列篩選] 索引標籤，選取資料表，然後按一下 [DAX 篩選] 欄位並輸入 DAX 公式。  
  
7.  若要將成員加入至角色，請按一下 [成員] 索引標籤，然後按一下 [加入]。  
  
    > [!NOTE]  
    >  您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，將角色成員加入至已部署的模型。 如需詳細資訊，請參閱[使用 SSMS 管理角色](../../analysis-services/tabular-models/manage-roles-by-using-ssms-ssas-tabular.md)。  
  
8.  在 [選取使用者或群組] 對話方塊中，輸入 Windows 使用者或 Windows 群組物件做為成員。  
  
9. 按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [檢視方塊](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [在 Excel 中進行分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)   
 [USERNAME 函數 (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f)   
 [CUSTOMDATA 函數 (DAX)](http://msdn.microsoft.com/en-us/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
  
  
