---
title: 第 1 課：建立報表伺服器專案 (Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 52050b9513de2638cacc394309f7e87d6ba77709
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56032359"
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>第 1 課：建立報表伺服器專案 (Reporting Services)
  若要在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中建立報表，必須先建立報表伺服器專案，您將在其中儲存報表定義 (.rdl) 檔案以及報表所需的任何其他資源檔案。 然後，您將建立實際的報表定義檔案、定義報表的資料來源、定義資料集，以及定義報表配置。 當您執行報表時，會擷取實際資料並與配置結合，然後轉譯在您的螢幕上，再從螢幕上匯出、列印或儲存資料。  
  
 在這一課，您將學習如何在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中建立報表伺服器專案。 報表伺服器專案用於建立在報表伺服器上執行的報表。  
  
### <a name="to-create-a-report-server-project"></a>建立報表伺服器專案  
  
1.  按一下 **開始**，指向**所有程式**，指向[!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]，然後按一下**SQL Server Data Tools**。 如果這是第一次您開啟[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]，按一下**商業智慧設定**預設環境設定。  
  
2.  在 [檔案]  功能表中，指向 [新增] ，然後按一下 [專案] 。  
  
3.  在 [已安裝的範本] 清單中，按一下 [商業智慧]。  
  
4.  按一下 **報表伺服器專案**。  
  
5.  在 [名稱] 中，輸入 **Tutorial**。  
  
6.  按一下 **[確定]** 建立專案。  
  
     Tutorial 專案隨即顯示在 [方案總管] 中。  
  
### <a name="to-create-a-new-report-definition-file"></a>建立新的報表定義檔案  
  
1.  在 [方案總管] 中，以滑鼠右鍵按一下**報表**，指向**新增**，然後按一下**新項目**。  
  
    > [!NOTE]  
    >  如果看不到方案總管視窗，請在 [檢視] 功能表上按一下方案總管。  
  
2.  在 **加入新項目**對話方塊的 **範本**，按一下 **報表**。  
  
3.  在 [名稱] 中，輸入 **Sales Orders.rdl** ，然後按一下 [新增] 。  
  
     報表設計師會在 [設計] 檢視中開啟並顯示新的 .rdl 檔案。  
  
 報表設計師是一個在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中執行的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]元件。 它有兩個檢視：**設計**並**預覽**。 按一下各個索引標籤，即可變更檢視。  
  
 您會在 [報表資料]  窗格中定義資料， 並在 [設計]  檢視中定義報表配置。 您可以執行報表，然後在 [預覽] 檢視中查看外觀。  
  
## <a name="next-task"></a>下一項工作  
 您已順利建立稱為 "Tutorial" 的報表專案，並將報表定義 (.rdl) 檔案加入至報表專案。 下一步，您將指定報表要用的資料來源。 請參閱[第 2 課：指定連接資訊&#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立基本資料表報表 &#40;SSRS 教學課程&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
