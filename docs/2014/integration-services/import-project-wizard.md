---
title: 匯入專案精靈 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.importprojectwizard.f1
ms.assetid: 9247ad6c-4bd1-43ab-b347-583181cb9917
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c4e18295d08797e4fa6b475d32ea2d688e187d91
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36147180"
---
# <a name="import-project-wizard"></a>匯入專案精靈
  使用 [ [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 匯入專案精靈] 即可根據現有的 Integration Services 專案建立新的專案。 您可以匯入已部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目錄的專案，或從專案部署檔案 (副檔名為 .ispac) 匯入專案。  
  
### <a name="to-create-a-project-based-on-a-project-in-ispac-file-or-in-catalog"></a>若要根據 .ispac 檔案或目錄中的專案建立專案  
  
1.  按一下 **[檔案]**、指向 **[新增]**，然後按一下 [專案]。  
  
2.  展開 **[商業智慧]**，然後按一下 **[Integration Services]**。  
  
3.  選取中間窗格的 **[Integration Services 匯入精靈]** 、輸入方案和專案的 **[名稱]** 、指定專案的 **[資料夾]** ，然後按一下 **[確定]**。  
  
     此時，您應該會看見 **[Integration Services 匯入專案精靈]**。 這個精靈會根據現有的 Integration Services 專案建立新的專案。  
  
4.  在 **[簡介]** 頁面上，按 **[下一步]** 即可看見 **[選取來源]** 頁面。  
  
5.  指定您想要從 .ispac 檔案或目錄匯入專案。  
  
    -   如果您選取 **[專案部署檔案]** 選項，請指定 .ispac 檔案的路徑。  
  
    -   如果您選取 **[Integration Services 目錄]** 選項，請指定目錄所在之資料庫伺服器執行個體的名稱，以及目錄中專案的路徑。  
  
6.  在 **[選取來源]** 頁面上，按 **[下一步]** 即可看見 **[檢閱]** 頁面。 在此頁面上檢閱精靈即將執行之匯入作業的相關資訊。  
  
7.  按一下 **[匯入]** ，根據您所選取的 Integration Services 專案建立新的專案。  
  
8.  **[結果]** 頁面應該會顯示精靈已執行之匯入作業的結果。 按一下 **[儲存報表]** ，將報表儲存至 XML 檔案。  
  
9. 按一下 **[關閉]** ，關閉精靈。  
  
  