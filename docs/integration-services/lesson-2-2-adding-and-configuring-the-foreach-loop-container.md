---
title: 步驟 2:新增和設定 Foreach 迴圈容器 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 88a973cc-0f23-4ecf-adb6-5b06279c2df6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0c865c00eb1020aa6128cdd7a40d61a191bad2a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65722738"
---
# <a name="lesson-2-2-add-and-configure-the-foreach-loop-container"></a>第 2-2 課：新增和設定 Foreach 迴圈容器

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在這個工作中，您要新增在一般檔案的資料夾中形成迴圈的功能，並對每個一般檔案套用第 1 課的資料流程轉換。 您的作法是在控制流程中加入和設定 Foreach 迴圈容器。  
  
您加入的 Foreach 迴圈容器必須能夠連接到資料夾的每個一般檔案。 由於資料夾的所有檔案都具有相同格式，所以 Foreach 迴圈容器可以使用相同的一般檔案連接管理員來連接每一個檔案。 容器會使用您在第 1 課建立的一般檔案連線管理員。  
  
目前，第 1 課中的一般檔案連線管理員只會連線到一個特定的一般檔案。 若要反覆連線到資料夾的每個一般檔案，您必須同時設定 Foreach 迴圈容器和一般檔案連線管理員，如下所示：  
  
-   **Foreach 迴圈容器：** 將容器的列舉值對應到使用者定義的套件變數。 容器接著會使用這個變數，動態地修改一般檔案連線管理員的 **ConnectionString** 屬性，並反覆連線到資料夾的每個一般檔案。  
  
-   **一般檔案連線管理員：** 使用使用者定義變數來填入連線管理員的 **ConnectionString** 屬性，以修改在第 1 課中建立的連線管理員。  
  
這個工作中的程序會向您說明如何建立和修改 Foreach 迴圈容器以使用使用者定義的套件變數，以及將資料流程工作新增到迴圈中。 在下一個工作中，您會學到如何修改一般檔案連線管理員來使用該使用者定義變數。  
  
對套件進行這些修改之後，當套件執行時，Foreach 迴圈容器會逐一查看範例資料夾內的所有檔案。 每次發現符合準則的檔案時，Foreach 迴圈容器就會以檔案名稱填入新的變數，將該變數對應到範例貨幣資料一般檔案連線管理員的 **ConnectionString** 屬性，然後對該檔案執行資料流程。 如此一來，在 Foreach 迴圈每次反覆運算時，資料流程工作都會取用不同的一般檔案。  
  
> [!NOTE]  
> 因為 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 隔開了控制流程與資料流程，所以您要新增到控制流程中的任何迴圈都不需要對資料流程進行修改。 因此，第 1 課的資料流程不必經過變更。  
  
## <a name="add-a-foreach-loop-container"></a>新增 Foreach 迴圈容器  
  
1.  在 **SQL Server Data Tools** 中，選取 [控制流程]  索引標籤。  
  
2.  在 [SSIS 工具箱]  中，展開 [容器]  ，然後將 [Foreach 迴圈容器]  拖曳至 [控制流程]  索引標籤的設計介面中。  
  
3.  以滑鼠右鍵按一下新的 [Foreach 迴圈容器]  ，並選取 [編輯]  。  
  
4.  在 [Foreach 迴圈編輯器]  對話方塊的 [一般]  頁面上，對 [名稱]  輸入 **Foreach File in Folder**。 選取 [確定]  。  
  
5.  以滑鼠右鍵按一下 Foreach 迴圈容器，選取 [屬性]  ，然後在 [屬性]  視窗中，確認 **LocaleID** 屬性是設為 [英文 (美國)]  。  
  
## <a name="configure-the-enumerator-for-the-foreach-loop-container"></a>設定 Foreach 迴圈容器的列舉程式  
  
1.  按兩下 [Foreach File in Folder]  ，來重新開啟 [Foreach 迴圈編輯器]  。  
  
2.  選取 [集合]  。  
  
3.  在 [集合]  頁面上，選取 [Foreach 檔案列舉值]  。  
  
4.  在 [列舉程式設定]  群組中，選取 [瀏覽]  。  
  
5.  在 [瀏覽資料夾]  對話方塊中，尋找電腦上包含 Currency_*.txt 檔案 (含有範例資料) 的資料夾。

6.  在 [檔案]  方塊中，輸入 **Currency_\*.txt**。  
  
## <a name="map-the-enumerator-to-a-user-defined-variable"></a>將列舉程式對應到使用者定義的變數  
  
1.  選取 [變數對應]  。  
  
2.  在 [變數對應]  頁面的 [變數]  欄位中，選取空白資料格，然後選取 [\<新增變數...>]  。  
  
3.  在 [新增變數]  對話方塊中，對 [名稱]  輸入 **varFileName**。  
  
    > [!NOTE]  
    > 變數名稱會區分大小寫。  
  
4.  選取 [確定]  。  
  
5.  再次選取 [確定]  來結束 [Foreach 迴圈編輯器]  對話方塊。  
  
## <a name="add-the-data-flow-task-to-the-loop"></a>將資料流程工作新增到迴圈  
  
-   將 [擷取範例貨幣資料]  資料流程工作拖曳到 **Foreach File in Folder** 這個 Foreach 迴圈容器。  
  
## <a name="go-to-next-task"></a>移至下一個工作  
[步驟 3：修改一般檔案連線管理員](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
## <a name="see-also"></a>另請參閱  
[設定 Foreach 迴圈容器](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)  
[在套件中使用變數](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
  
