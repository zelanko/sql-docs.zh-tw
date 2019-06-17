---
title: 第 2 課：使用 xsd 工具的 RDL 結構描述產生類別 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a81c87f1-7977-4b30-b6ac-b38b3e2b6398
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f5f74c6621d329885e9149fce9a37c7418d9c37b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62653749"
---
# <a name="lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool"></a>第 2 課：使用 xsd 工具，從 RDL 結構描述產生類別
  建立 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 專案之後，下一個步驟就是擷取報表定義結構描述的本機副本，並執行 XML 結構描述定義工具 (Xsd.exe)。  
  
### <a name="to-generate-the-rdl-classes"></a>產生 RDL 類別  
  
1.  開啟的執行個體[!INCLUDE[msCoName](../includes/msconame-md.md)]Internet Explorer （或對等的網頁瀏覽器），並瀏覽至下列 URL:  
  
    ```  
    https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition/ReportDefinition.xsd  
    ```  
  
2.  一旦在瀏覽器中開啟 RDL 結構描述後，瀏覽至**檔案**功能表，然後選取**另存新檔**。  
  
3.  瀏覽至建立 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 專案的位置，然後以 ReportDefinition.xsd 檔案名稱儲存結構描述。  
  
4.  在儲存檔案後，開啟的執行個體[!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]命令提示字元。 若要開啟命令提示字元的執行個體，請按一下 [開始] 功能表，指向**所有程式**，指向**Microsoft Visual Studio 2010**，指向**Visual Studio Tools**按一下**Visual Studio 命令提示字元 (2010)** 。  
  
5.  變更目前路徑至儲存 ReportDefinition.xsd 檔案的位置：  
  
     `CD\<ReportDefinition.xsd Path>`  
  
6.  以下列命令產生其中包含 RDL 結構描述類別的 ReportDefinition.cs 檔案：  
  
     `xsd /c /n:SampleRDLSchema ReportDefinition.xsd`  
  
     若要使用此命令產生 ReportDefinition.vb 檔：  
  
     `xsd /c /l:VB /n:SampleRDLSchema ReportDefinition.xsd`  
  
7.  將 ReportDefinition.xsd 加入至您的專案。 從**專案**功能表上，按一下**加入現有項目**。 瀏覽至 ReportDefinition.xsd 檔案的位置、 選取 ReportDefinition.xsd，然後按一下**新增**。  
  
    > [!NOTE]  
    >  ReportDefinition.xsd 檔案加入專案之後，您會發現**方案總管 中**，ReportDefinition.cs (.vb) 檔案不存在。 若要顯示檔案，請按一下 ReportDefinition.xsd 檔案旁邊的展開/摺疊按鈕。  
  
## <a name="next-lesson"></a>下一課  
 在下一課，您將撰寫程式碼，使用您從 RDL 結構描述產生的類別，從報表伺服器載入報表定義。 請參閱[第 3 課：從報表伺服器載入報表定義](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用從 RDL 結構描述產生的類別更新報表&#40;SSRS 教學課程&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [報表定義語言 &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
