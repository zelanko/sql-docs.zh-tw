---
title: 步驟 2：新增和設定 Foreach 迴圈容器 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 88a973cc-0f23-4ecf-adb6-5b06279c2df6
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dcbdf3baf515ac83a4910193ef0bd25b8f3f597a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="lesson-2-2---adding-and-configuring-the-foreach-loop-container"></a>課程 2-2 - 新增和設定 Foreach 迴圈容器
在這項工作中，您將加入功能，於一般檔案的資料夾中形成迴圈，並對每個一般檔案套用在第 1 課使用的相同資料流程轉換。 您的作法是在控制流程中加入和設定 Foreach 迴圈容器。  
  
您加入的 Foreach 迴圈容器必須能夠連接到資料夾的每個一般檔案。 由於資料夾的所有檔案都具有相同格式，所以 Foreach 迴圈容器可以使用相同的一般檔案連接管理員來連接每一個檔案。 容器要使用的一般檔案連接管理員與您在第 1 課建立的一般檔案連接管理員相同。  
  
目前，第 1 課的一般檔案連接管理員只連接一個特定的一般檔案。 若要反覆連接到資料夾的每個一般檔案，您必須同時設定 Foreach 迴圈容器和一般檔案連接管理員，如下所示：  
  
-   **Foreach 迴圈容器** ：您將容器的列舉值對應至使用者定義的套件變數。 然後容器會使用此使用者自訂變數，動態修改一般檔案連接管理員的 **ConnectionString** 屬性，並反覆連接到資料夾的每個一般檔案。  
  
-   **一般檔案連接管理員** ：您將使用使用者定義變數來擴展連接管理員的 **ConnectionString** 屬性，以修改第 1 課所建立的連接管理員。  
  
這項工作中的程序說明如何建立和修改 Foreach 迴圈容器，以利用使用者自訂封裝變數，並且將資料流程工作加入迴圈中。 在下一項工作中，您會學到如何修改一般檔案連接管理員來使用使用者自訂變數。  
  
對封裝做了這些修改之後，當封裝執行時，Foreach 迴圈容器將反覆進行範例資料夾內的檔案集合。 每次發現符合準則的檔案時，Foreach 迴圈容器就會在使用者自訂變數中填入檔案名稱，將使用者自訂變數對應至 [範例貨幣資料一般檔案] 連接管理員的 **ConnectionString** 屬性，然後對該檔案執行資料流程。 因此，在 Foreach 迴圈的每個反覆運算中，資料流程工作將取用不同的一般檔案。  
  
> [!NOTE]  
> 因為 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 隔開控制流程與資料流程，所以您要加入控制流程中的任何迴圈都不需要對資料流程做修改。 因此，您在第 1 課建立的資料流程不必改變。  
  
### <a name="to-add-a-foreach-loop-container"></a>若要加入 Foreach 迴圈容器  
  
1.  在 SQL Server Data Tools 中，請按一下 [控制流程] 索引標籤。  
  
2.  在 [SSIS 工具箱] 中，展開 [容器]，然後將 [Foreach 迴圈容器] 拖曳至 [控制流程] 索引標籤的設計介面中。  
  
3.  以滑鼠右鍵按一下剛新增的 [Foreach 迴圈容器]，並選取 [編輯]。  
  
4.  在 [Foreach 迴圈編輯器] 對話方塊的 [一般] 頁面上，對 [名稱] 輸入 **Foreach File in Folder**。 按一下 [確定] 。  
  
5.  以滑鼠右鍵按一下 [Foreach 迴圈] 容器，按一下 [屬性]，然後在 [屬性] 視窗中，確認 **LocaleID** 屬性是設為 [英文 (美國)]。  
  
### <a name="to-configure-the-enumerator-for-the-foreach-loop-container"></a>若要設定 Foreach 迴圈容器的列舉值  
  
1.  按兩下 [資料夾的 Foreach 檔案]，來重新開啟 [Foreach 迴圈編輯器]。  
  
2.  按一下 [集合]。  
  
3.  在 [集合] 頁面上，選取 [Foreach 檔案列舉值]。  
  
4.  在 [列舉值組態] 群組中，按一下 [瀏覽]。  
  
5.  在 [瀏覽資料夾] 對話方塊中，尋找電腦上包含 Currency_*.txt 檔案的資料夾。  
  
    此範例資料隨附在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 課程封裝中。 若要下載範例資料和課程封裝，請執行下列動作。  
  
    1.  導覽至 [Integration Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=275027)。 
  
    2.  按一下 **[下載]** 索引標籤。  
  
    3.  按一下 [SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip](http://msftisprodsamples.codeplex.com/downloads/get/596031) 檔案的連結。  
  
6.  在 [檔案] 方塊中，輸入 **Currency_\*.txt**。  
  
### <a name="to-map-the-enumerator-to-a-user-defined-variable"></a>若要將列舉值對應至使用者自訂變數  
  
1.  按一下 [變數對應]。  
  
2.  在 [變數對應] 頁面的 [變數] 資料行中，按一下空白資料格，然後選取 [\<新增變數...>]。  
  
3.  在 [新增變數] 對話方塊中，對 [名稱] 輸入 **varFileName**。  
  
    > [!IMPORTANT]  
    > 變數名稱會區分大小寫。  
  
4.  按一下 [確定] 。  
  
5.  再按一下 [確定] 來結束 [Foreach 迴圈編輯器] 對話方塊。  
  
### <a name="to-add-the-data-flow-task-to-the-loop"></a>若要將資料流程工作加入迴圈中  
  
-   將 [擷取範例貨幣資料] 資料流程工作拖曳至 Foreach 迴圈容器，這個容器現在已重新命名為 [資料夾的 Foreach 檔案]。  
  
## <a name="next-lesson-task"></a>下一課的工作  
[步驟 3：修改一般檔案連接管理員](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
## <a name="see-also"></a>另請參閱  
[設定 Foreach 迴圈容器](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)  
[在封裝中使用變數](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
  
