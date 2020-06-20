---
title: 匯入 Integration Services 專案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3301c328-b0f5-4517-915c-93713413e453
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5191da78fc32d72c54fa6da925bd419685b90152
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965658"
---
# <a name="import-an-integration-services-project"></a>匯入 Integration Services 專案
  使用 [[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 匯入專案精靈]**** 從現有的部署檔 (.ispac)，或從部署到 Integration Services 目錄的專案建立一個專案。 當您沒有專案的原始副本，但又想從 .ispac 檔或 SSISDB 目錄建立一個專案時，此功能特別有用。  
  
### <a name="to-import-a-project"></a>若要匯入專案  
  
1.  在中 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ， **New**按一下 [檔案]  >  功能表上的 [新增**專案**]。 **File**  
  
2.  在 **[新增專案]** 視窗的 **[已安裝的範本]** 區域中，展開 **[Business Intelligence]**，然後按一下 **[Integration Services]**。  
  
3.  從專案類型清單中選取 **[Integration Services 匯入專案精靈]** 。  
  
4.  在 **[名稱]** 文字方塊中，為要建立的新專案輸入一個名稱。  
  
5.  在 **[位置]** 文字方塊中輸入專案的路徑或位置，或按一下 **[瀏覽]** 來選取一個路徑或位置。  
  
6.  在 **[方案名稱]** 文字方塊中輸入方案的名稱。  
  
7.  按一下 **[確定]** ，啟動 **[Integration Services 匯入專案精靈]** 對話方塊。  
  
8.  按 **[下一步]** ，切換到 **[選取來源]** 頁面。  
  
9. 如果您要從 **.ispac** 檔匯入，請在 **[路徑]** 文字方塊中輸入路徑，包括檔案名稱。 按一下 **[瀏覽]** 導覽到您希望儲存方案的資料夾，並在 **[檔案名稱]** 文字方塊中輸入檔案名稱，然後按一下 **[開啟]**。  
  
     如果您要從 **[Integration Services 目錄]** 匯入，請在 **[伺服器名稱]** 文字方塊中輸入資料庫執行個體名稱，或按一下 **[瀏覽]** ，然後選取包含該目錄的資料庫執行個體。  
  
     按一下 **[路徑]** 文字方塊旁的 **[瀏覽]** 、展開目錄中的資料夾、選取您要匯入的專案，然後按一下 **[確定]**。  
  
     按 **[下一步]** ，切換到 **[檢閱]** 頁面。  
  
10. 檢閱資訊，然後按一下 **[匯入]** ，即可根據您所選取的現有專案建立一個專案。  
  
11. 選擇性：按一下 **[儲存報表]** ，將結果儲存到檔案中。  
  
12. 按一下 **[關閉]** ，關閉 **[Integration Services 匯入專案精靈]** 對話方塊。  
  
  
