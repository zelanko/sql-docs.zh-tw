---
title: Analysis Services 教學課程第 1 課： 建立新的表格式模型專案 |Microsoft Docs
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df9595071c60680db94a18dc373ce24f1f9b4ea5
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43108667"
---
# <a name="create-a-tabular-model-project"></a>建立表格式模型專案

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您使用 Visual Studio 與 SQL Server Data Tools (SSDT) 或 Visual Studio 2017 與 Microsoft Analysis Services 專案 VSIX 1400 相容性層級建立新的表格式模型專案。 一旦建立新的專案時，就可以開始加入資料，並撰寫您的模型。 這一課也可讓您的表格式模型撰寫環境，在 Visual Studio 中的簡介。  
  
完成本課程的估計時間： **10 分鐘**  
  
## <a name="prerequisites"></a>先決條件

這篇文章是在表格式模型撰寫教學課程第 1 課。 若要完成本課程中，有幾項必要條件，您需要備妥。 若要進一步了解，請參閱[Analysis Services-Adventure Works 教學課程](../tutorial-tabular-1400/as-adventure-works-tutorial.md)。  
  
## <a name="create-a-new-tabular-model-project"></a>建立新的表格式模型專案  
  
#### <a name="to-create-a-new-tabular-model-project"></a>若要建立新的表格式模型專案  
  
1.  在 Visual Studio 中，在**檔案**功能表上，按一下**新增** > **專案**。  
  
2.  在 **新的專案**對話方塊方塊中，展開**已安裝** > **Business Intelligence** > **Analysis Services**，然後按一下**Analysis Services 表格式專案**。  
  
3.  在 **名稱**，型別**AW 網際網路銷售**，然後指定專案檔案的位置。  
  
    根據預設，**方案名稱**等同於專案名稱; 不過，您可以輸入不同的解決方案名稱。  
  
4.  按一下 [確定] 。  
  
5.  在 **表格式模型設計師**對話方塊中，選取**整合式工作區**。  
  
    工作區會裝載與專案同名的表格式模型資料庫，在模型製作期間。 整合式工作區意味著 Visual Studio 會使用內建的執行個體，不需要安裝個別的 Analysis Services 伺服器執行個體，只為了撰寫模型。
      
6.  在 **相容性層級**，選取**SQL Server 2017 / Azure Analysis Services (1400)**。   
 
    ![as-lesson1-tmd](../tutorial-tabular-1400/media/as-lesson1-tmd.png)
      
    如果您沒有看到 SQL Server 2017 / Azure Analysis Services (1400) 相容性層級的清單方塊中，您不使用最新版的 SQL Server Data Tools。 若要取得最新版本，請參閱 [安裝 SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)。  
      
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>了解 SSDT 表格式模型撰寫環境  

既然您已建立新的表格式模型專案，讓我們花一點時間瀏覽表格式模型撰寫環境，在 Visual Studio 中。  
  
您的專案建立之後，它會開啟在 Visual Studio 中。 在右側中，在**表格式模型總管**，您會看到樹狀檢視的物件模型中。 您還沒有匯入資料，所以資料夾是空的。 您可以滑鼠右鍵按一下來執行動作，類似於功能表列物件資料夾。 當您逐步執行本教學課程中，您可以使用表格式模型總管 來瀏覽模型專案中的不同的物件。

![as-lesson1-tme](../tutorial-tabular-1400/media/as-lesson1-tme.png)

按一下 **方案總管 中** 索引標籤。您可以看到您**Model.bim**檔案。 如果您看不到左 （含有 [Model.bim] 索引標籤的空視窗），設計工具視窗中**方案總管**下方**AW 網際網路銷售專案**，連按兩下**Model.bim**檔案。 Model.bim 檔案包含模型專案的中繼資料。 

![做為第 1 課 se](../tutorial-tabular-1400/media/as-lesson1-se.png)
  
按一下 **方案總管**中建立新的空白表格式模型專案。 在 [**屬性**] 視窗中，您會看到模型屬性，最重要的是**DirectQuery 模式**屬性。 此屬性會指定是否在記憶體中模式 （關閉） 還是 DirectQuery 模式 （開啟） 部署模型。 本教學課程中，您可以撰寫和部署於記憶體中模式的模型。

![做為第 1 課屬性](../tutorial-tabular-1400/media/as-lesson1-properties.png)
  
當您建立的模型專案時，根據資料模型化，可以指定自動設定某些模型屬性**工具**功能表 >**選項** 對話方塊。 [資料備份]、[工作空間保留] 和 [工作空間伺服器] 屬性會指定備份、在記憶體中保留以及建立工作空間資料庫 (您的模型撰寫資料庫) 的方式和位置。 您可以稍後變更這些設定，如有必要，但現在，請保留這些屬性時。  

在 [**方案總管] 中**，以滑鼠右鍵按一下**AW 網際網路銷售**（專案），然後按一下**屬性**。 **AW 網際網路銷售屬性頁** 對話方塊隨即出現。 您稍後部署模型時設定其中部分屬性的。  
  
當您安裝 SSDT 時，數個新的功能表項目已新增至 Visual Studio 環境中。 按一下 **模型**功能表。 從這裡開始，您可以匯入資料、 重新整理工作區的資料、 瀏覽您在 Excel 中的模型、 建立檢視方塊和角色、 選取模型檢視，以及設定計算選項。 按一下 **資料表**功能表。 從這裡開始，您可以建立和管理關聯性、 指定日期資料表設定、 建立磁碟分割，和編輯資料表屬性。 如果您按一下**資料行** 功能表中，您可以加入和刪除資料表中的資料行、 凍結資料行，以及指定排序次序。 SSDT 也會新增某些按鈕列。 最好是使用自動加總 」 功能，來建立所選取的資料行的標準彙總量值。 其他工具列按鈕可讓您快速存取常用的功能和命令。  
  
瀏覽撰寫表格式模型之各種不同專屬功能的對話方塊和位置。 雖然某些項目目前尚未使用，您可以取得實用的表格式模型撰寫環境。  
  

## <a name="whats-next"></a>下一步

[第 2 課： 取得資料](../tutorial-tabular-1400/as-lesson-2-get-data.md)。

  
  
  
