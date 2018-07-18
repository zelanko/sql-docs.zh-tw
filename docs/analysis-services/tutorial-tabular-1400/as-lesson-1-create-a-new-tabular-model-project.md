---
title: Analysis Services 教學課程第 1 課： 建立新的表格式模型專案 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 403e6d04d339e3126afe964bd919304d04295c0b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044192"
---
# <a name="create-a-tabular-model-project"></a>建立表格式模型專案

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您使用 Visual Studio 與 SQL Server Data Tools (SSDT) 或與 Microsoft Analysis Services 專案 VSIX 的 Visual Studio 2017 1400年相容性層級建立新的表格式模型專案。 一旦建立新專案之後，您就可以開始加入資料，並撰寫您的模型。 這一課也可讓您的表格式模型撰寫環境，在 Visual Studio 中的簡介。  
  
完成本課程的估計時間：**10 分鐘**  
  
## <a name="prerequisites"></a>필수 구성 요소

本文是表格式模型撰寫教學課程中的第 1 課。 若要完成本課程中，有幾項必要條件，則必須先在就地。 若要進一步了解，請參閱[Analysis Services-Adventure Works 教學課程](../tutorial-tabular-1400/as-adventure-works-tutorial.md)。  
  
## <a name="create-a-new-tabular-model-project"></a>建立新的表格式模型專案  
  
#### <a name="to-create-a-new-tabular-model-project"></a>若要建立新的表格式模型專案  
  
1.  在 Visual Studio 中，在**檔案**功能表上，按一下 **新增** > **專案**。  
  
2.  在**新專案**對話方塊方塊中，展開 **已安裝** > **Business Intelligence** > **Analysis Services**，然後按一下  **Analysis Services 表格式專案**。  
  
3.  在**名稱**，型別**AW Internet Sales**，然後指定專案檔案的位置。  
  
    根據預設，**方案名稱**等同於專案名稱; 不過，您可以輸入不同的方案名稱。  
  
4.  按一下 **[確定]**。  
  
5.  在**表格式模型設計師**對話方塊中，選取**整合式工作區**。  
  
    工作區在模型製作期間裝載表格式模型資料庫與專案名稱相同。 整合式工作區表示 Visual Studio 會使用內建的執行個體，因而不須安裝個別的 Analysis Services 伺服器執行個體，只能用來撰寫模型。
      
6.  在**相容性層級**，選取**SQL Server 2017 / Azure Analysis Services (1400)**。   
 
    ![as-lesson1-tmd](../tutorial-tabular-1400/media/as-lesson1-tmd.png)
      
    如果看不到 SQL Server 2017 / Azure Analysis Services (1400) 相容性層級清單方塊中的，您不使用最新版的 SQL Server Data Tools。 若要取得最新版本，請參閱 [安裝 SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)。  
      
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>了解在 SSDT 的表格式模型撰寫環境  

既然您已建立新的表格式模型專案，讓我們花一點時間瀏覽表格式模型撰寫 Visual Studio 中的環境。  
  
您的專案建立之後，它會在 Visual Studio 中開啟。 在右側，在**表格式模型總管**，即在您的模型中之物件的樹狀檢視。 您還沒有匯入資料，因為資料夾會是空的。 您可以滑鼠右鍵按一下要執行動作，類似於功能表列物件的資料夾。 當您逐步執行本教學課程中，您可以使用表格式模型總管 來瀏覽在模型專案中的不同物件。

![as-lesson1-tme](../tutorial-tabular-1400/media/as-lesson1-tme.png)

按一下**方案總管 中** 索引標籤。您可以看到您**Model.bim**檔案。 如果您看不到左 （Model.bim 索引標籤的空視窗），設計工具視窗中**方案總管 中**下**AW Internet Sales 專案**，連按兩下**Model.bim**檔案。 Model.bim 檔案包含您的模型專案的中繼資料。 

![做為第 1 課 se](../tutorial-tabular-1400/media/as-lesson1-se.png)
  
按一下 **方案總管**中建立新的空白表格式模型專案。 在**屬性**視窗中，您會看見模型屬性，最重要的是**DirectQuery 模式**屬性。 此屬性會指定是否在記憶體中模式 （關閉） 或是 DirectQuery 模式 （開啟） 部署模型。 本教學課程，您可以撰寫和部署記憶體中模式的模型。

![做為第 1 課屬性](../tutorial-tabular-1400/media/as-lesson1-properties.png)
  
當您建立模型專案時，根據資料模型化，可以指定自動設定某些模型屬性**工具**功能表 >**選項** 對話方塊。 [資料備份]、[工作空間保留] 和 [工作空間伺服器] 屬性會指定備份、在記憶體中保留以及建立工作空間資料庫 (您的模型撰寫資料庫) 的方式和位置。 您可以稍後變更這些設定，如有必要，但現在，這些屬性保持不變。  

在**方案總管] 中**，以滑鼠右鍵按一下**AW Internet Sales** （專案），然後按一下 [**屬性**。 **AW Internet Sales 屬性頁** 對話方塊隨即出現。 您稍後在部署模型時設定其中部分屬性的。  
  
當您安裝 SSDT 時，數個新的功能表項目已加入至 Visual Studio 環境中。 按一下**模型**功能表。 從這裡，您可以匯入資料、 重新整理工作區中的資料、 瀏覽您在 Excel 中的模型、 建立檢視方塊和角色、 選取模型檢視，以及設定計算選項。 按一下**資料表**功能表。 從這裡，您可以建立及管理關聯性、 指定日期資料表設定、 建立磁碟分割，和編輯資料表屬性。 如果您按一下**資料行**功能表上，您可以加入和刪除資料表中的資料行、 凍結資料行，以及指定排序次序。 SSDT 也會加入一些按鈕到列。 最有用的是 [自動加總] 功能建立標準彙總的量值所選取的資料行。 其他工具列按鈕可讓您快速存取常用的功能和命令。  
  
瀏覽撰寫表格式模型之各種不同專屬功能的對話方塊和位置。 雖然某些項目尚無法使用中，您可以取得充分了解表格式模型撰寫環境。  
  

## <a name="whats-next"></a>下一步

[第 2 課： 取得資料](../tutorial-tabular-1400/as-lesson-2-get-data.md)。

  
  
  
