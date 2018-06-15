---
title: 授與處理權限 (Analysis Services) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c855bf2ecc14490b2298cf1fa240509a07369cf1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024065"
---
# <a name="grant-process-permissions-analysis-services"></a>授與處理權限 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  身為管理員，您可以建立專用於 Analysis Services 處理作業的角色，讓您能夠將該特殊工作委派給其他使用者，或委派給用於自動排程處理的應用程式。 處理權限可在資料庫、Cube、維度和採礦結構層級上授與。 除非您正在使用一個非常大的 Cube 或表格式資料庫，否則建議在資料層級授與處理權限，內含所有物件，包含彼此間具有相依性的物件。  
  
 權限是透過將物件與權限和 Windows 使用者或群組帳戶關聯的角色來授與。 請記住，權限是加總的。 如果某個角色會授與處理 Cube 的權限，第二個角色則提供處理維度的相同使用者權限時，在兩個不同角色的權限結合之後，使用者即擁有處理 Cube 及處理該資料庫內之指定維度的權限。  
  
> [!IMPORTANT]  
>  角色僅擁有 [處理] 權限的使用者將無法使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 及處理物件。 這些工具需要有 **讀取定義** 權限來存取物件中繼資料。 如果無法使用這些工具，就必須使用 XMLA 指令碼來執行處理作業。  
>   
>  建議您基於測試目的，同時授與 **讀取定義** 權限。 擁有 **讀取定義** 和 **處理資料庫** 權限的使用者可以透過互動方式處理 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的物件。 如需詳細資訊，請參閱 [授與物件中繼資料的讀取定義權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md) 。  
  
## <a name="set-processing-permissions-at-the-database-level"></a>設定資料庫層級的處理權限  
 本節說明如何針對資料庫中的所有 Cube、維度、採礦結構及採礦模型，由非管理員的使用者來啟用處理。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體、開啟 [資料庫] 資料夾，然後選取資料庫。  
  
2.  以滑鼠右鍵按一下**角色** | **新角色**。 輸入名稱和描述。  
  
3.  在 [一般] 窗格中，選取 [處理資料庫] 核取方塊。 此外，選取 [讀取定義]，也會透過某一個 SQL Server 工具啟用互動式處理，例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
4.  在 [成員資格] 窗格中，新增擁有權限可處理這個資料庫中任何物件的 Windows 使用者和群組帳戶。  
  
5.  按一下 [確定] 以完成角色定義。  
  
## <a name="set-processing-permissions-on-individual-objects"></a>設定個別物件的處理權限  
 您可以設定個別 Cube、維度、資料採礦結構或模型的處理權限。  
  
 如果您不小心排除了需要一起處理的物件 (例如，如果您啟用 Cube 上的處理，但未啟用其相關維度上的處理)，則處理會失敗。 因為很容易遺失物件相依性，因此，在設定個別物件的處理權限時，徹底測試是必要的。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的執行個體、開啟 [資料庫] 資料夾，然後選取資料庫。  
  
2.  以滑鼠右鍵按一下**角色** | **新角色**。 輸入名稱和描述。  
  
3.  在 [一般] 窗格中，清除 [處理資料庫] 核取方塊。 資料庫權限會藉由將角色選項變成灰色或無法選取狀態，來覆寫設定較低層級物件之權限的能力。  
  
     技術上來說，專屬的處理角色不需要任何資料庫權限。 但是，如果沒有資料庫層級的 [讀取定義]，您就無法檢視 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的資料庫，讓測試更為困難。  
  
4.  選取要處理的個別物件：  
  
    -   在 [Cube] 窗格中，選取每個 Cube 的 [處理] 核取方塊。  
  
    -   在 [維度] 窗格中，選取 [所有資料庫維度]，然後選取每個維度的 [處理] 核取方塊。 或者，選取所有資料列，然後使用 Shift + 滑鼠左鍵來切換核取方塊選取項目。  
  
5.  在 [成員資格] 窗格中，新增擁有權限可處理這些物件的 Windows 使用者和群組帳戶。  
  
6.  按一下 [確定] 以完成角色定義。  
  
## <a name="test-processing"></a>測試處理  
  
1.  按住 Shift 鍵並使用滑鼠右鍵按一下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、選取 [以不同的使用者身分執行]，然後使用指派給您正在測試之角色的 Windows 帳戶連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體。  
  
2.  開啟 [資料庫] 資料夾，然後選取資料庫。 您將只會看見您的帳戶具有成員資格之角色可看見的資料庫。  
  
3.  使用滑鼠右鍵按一下 Cube 或維度，然後選取 [處理]。 選擇處理選項。 針對所有物件組合，測試所有選項。 如果因為遺漏物件而發生錯誤，請將物件新增到角色。  
  
## <a name="set-processing-permissions-on-a-data-mining-structure"></a>設定資料採礦結構的處理權限  
 您可以建立角色，授與權限來處理資料採礦結構。 其中包括處理所有採礦模型。  
  
 可用來瀏覽採礦模型和結構的 [鑽研] 和 [讀取定義] 權限是不可部分完成的，而且可新增到同一個角色，或者分離到不同的角色。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的執行個體、開啟 [資料庫] 資料夾，然後選取資料庫。  
  
2.  以滑鼠右鍵按一下**角色** | **新角色**。 輸入名稱和描述。 在 [一般] 窗格中，確定已取消選取資料庫權限核取方塊。 資料庫權限將會藉由將角色選項變成灰色或無法選取狀態，來覆寫設定較低層級物件之權限的能力。  
  
3.  在 [採礦結構] 窗格中，選取每個採礦結構的 [處理] 核取方塊。  
  
4.  在 [成員資格] 窗格中，新增擁有可處理這個資料庫中任何物件之權限的 Windows 使用者和群組帳戶。  
  
5.  按一下 [確定] 以完成角色定義。  
  
## <a name="see-also"></a>另請參閱  
 [處理資料庫、資料表或資料分割 &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)   
 [處理多維度模型 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Grant 資料庫權限 & #40;Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)   
 [授與的讀取定義權限的物件中繼資料 & #40;Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
  
