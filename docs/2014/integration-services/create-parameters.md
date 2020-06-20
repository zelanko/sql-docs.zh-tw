---
title: 建立參數 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.parameterwindow.f1
ms.assetid: cd5d675b-dd5d-49cc-8b1f-dc717a973f99
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f43c6f25d7360b558a8bbfb9887b6bd2d6362106
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84917215"
---
# <a name="create-parameters"></a>Create Parameters
  您可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 來建立專案參數和封裝參數。 下列程序會提供建立封裝/專案參數的逐步指示。  
  
> [!NOTE]  
>  如果要將使用舊版 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 建立的專案轉換為專案部署模型，可以使用 **[Integration Services 專案轉換精靈]** ，根據組態建立參數。 如需詳細資訊，請參閱 [將專案部署至 Integration Services 伺服器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)。  
  
### <a name="to-create-package-parameters"></a>若要建立封裝參數  
  
1.  開啟 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中的封裝，然後按一下 SSIS 設計師中的 **[參數]** 索引標籤。  
  
     ![套件的 [參數] 索引標籤](media/denali-package-parameters.gif "套件的 [參數] 索引標籤")  
  
2.  按一下工具列上的 **[加入參數]** 按鈕。  
  
     ![新增工具列按鈕](media/denali-parameter-add.gif "新增工具列按鈕")  
  
3.  在清單本身或 **[屬性]** 視窗中，輸入 **[名稱]**、 **[資料類型]**、 **[值]**、 **[區分]** 以及 **[必要]** 屬性的值。 下表描述這些屬性。  
  
    |屬性|描述|  
    |--------------|-----------------|  
    |名稱|參數名稱。|  
    |資料類型|參數的資料類型。|  
    |預設值|在設計時指派的參數預設值。 這也稱為設計預設值。|  
    |敏感|敏感性參數值會在目錄中加密，以 Transact-SQL 或 SQL Server Management Studio 來檢視時，會顯示為 NULL 值。|  
    |必要|必須先指定一個值 (非設計預設值)，封裝才能執行。|  
    |描述|為方便維護，使用參數的描述。 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，於 Visual Studio 的 [屬性] 視窗中設定參數描述 (已在適用的參數視窗中選取參數)。|  
  
    > [!NOTE]  
    >  當您將專案部署至目錄時，會再多幾個屬性與專案相關聯。 若要查看目錄中所有參數的所有屬性，請使用 [catalog.object_parameters &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database) 檢視。  
  
4.  儲存專案以儲存參數的變更。 參數值會儲存在專案檔案中。  
  
    > [!WARNING]  
    >  您可以在清單中就地編輯，也可以使用 [屬性]**** 視窗來修改參數屬性的值。 您可以使用 [刪除] **(X)** 工具列按鈕來刪除參數。 您可以使用最後一個工具列按鈕，為僅在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中執行包時使用的參數指定值。  
  
    > [!NOTE]  
    >  如果您在沒有開啟 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中專案的情況下重新開啟封裝檔案，[參數]**** 索引標籤將會是空的，而且遭到停用。  
  
### <a name="to-create-project-parameters"></a>若要建立專案參數  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中開啟專案。  
  
2.  以滑鼠右鍵按一下方案總管中的 **Project.params**，然後按一下 [開啟]**** \(或) 按兩下 **Project.params** 來開啟它。  
  
     ![專案參數視窗](media/denali-project-parameters.gif "專案參數視窗")  
  
3.  按一下工具列上的 **[加入參數]** 按鈕。  
  
     ![新增工具列按鈕](media/denali-parameter-add.gif "新增工具列按鈕")  
  
4.  輸入 **[名稱]**、 **[資料類型]**、 **[值]**、 **[區分]** 以及 **[必要]** 屬性的值。  
  
    |屬性|描述|  
    |--------------|-----------------|  
    |名稱|參數名稱。|  
    |資料類型|參數的資料類型。|  
    |預設值|在設計時指派的參數預設值。 這也稱為設計預設值。|  
    |敏感|敏感性參數值會在目錄中加密，以 Transact-SQL 或 SQL Server Management Studio 來檢視時，會顯示為 NULL 值。|  
    |必要|必須先指定一個值 (非設計預設值)，封裝才能執行。|  
    |描述|為方便維護，使用參數的描述。 在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，於 Visual Studio 的 [屬性] 視窗中設定參數描述 (已在適用的參數視窗中選取參數)。|  
  
5.  儲存專案以儲存參數的變更。 參數值儲存在專案檔案的組態中。 儲存專案檔案即可將參數值的任何變更認可到磁碟。  
  
    > [!WARNING]  
    >  您可以在清單中就地編輯，也可以使用 [屬性]**** 視窗來修改參數屬性的值。 您可以使用 [刪除] **(X)** 工具列按鈕來刪除參數。 使用最後一個工具列按鈕開啟 **[管理參數值]** 對話方塊，針對僅在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中執行封裝時使用的參數指定值。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 參數](integration-services-ssis-package-and-project-parameters.md)  
  
  
