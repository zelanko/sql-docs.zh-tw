---
title: 在子封裝中使用變數和參數的值 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- configurations [Integration Services]
- packages [Integration Services], configurations
- variables [Integration Services], adding
ms.assetid: 9b939edb-4e17-48e5-8428-855beb10049c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2425c15428dbaa05e9d29b2d9a89f8fc7d68f6c7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054725"
---
# <a name="use-the-values-of-variables-and-parameters-in-a-child-package"></a>在子封裝中使用變數和參數的值
  此程序描述如何建立使用父變數組態類型的封裝組態。 此組態類型可讓從父封裝執行的子封裝存取父變數。  
  
> [!NOTE]  
>  您也可以設定 [執行封裝工作] 將父封裝變數或參數 (或專案參數) 對應到子封裝參數，以將值傳遞到子封裝。 如需詳細資訊，請參閱 [執行封裝工作](control-flow/execute-package-task.md)。  
  
 在子封裝中建立封裝組態之前，並不需要在父封裝中建立變數。 您可以隨時將變數加入父封裝中，但是必須使用封裝組態中父變數的確切名稱。 不過，在可以更新組態的子封裝中必須包含現有的變數，您才可以建立父變數組態。 如需加入和設定變數的詳細資訊，請參閱 [加入、刪除、變更封裝中使用者定義變數的範圍](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)。  
  
 父變數組態使用之父封裝中變數的範圍可以設定為「執行封裝」工作、擁有該工作的容器，或是封裝。 如果封裝中定義了多個名稱相同的變數，則會使用最接近「執行封裝」工作範圍的變數。 最接近「執行封裝」工作的範圍就是工作本身。  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>若要將變數加入父封裝  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含要加入用來傳遞到子封裝之變數的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [ [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中，若要定義變數的範圍，請執行下列其中之一：  
  
    -   若要將範圍設為封裝，請按一下 [控制流程]**** 索引標籤之設計介面上的任意位置。  
  
    -   若要將範圍設定為「執行封裝」工作的父容器，請按一下該容器。  
  
    -   若要將範圍設定為「執行封裝」，請按一下該工作。  
  
4.  加入及設定變數。  
  
    > [!NOTE]  
    >  選取與變數所要儲存之資料相容的資料類型。  
  
5.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="to-add-a-variable-to-a-child-package"></a>若要將變數加入子封裝  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含要加入父變數組態之封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，若要將範圍設定為封裝，請按一下 [控制流程]**** 索引標籤之設計介面上的任意位置。  
  
4.  加入及設定變數。  
  
    > [!NOTE]  
    >  選取與變數所要儲存之資料相容的資料類型。  
  
5.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="to-add-a-parent-package-configuration-to-a-child-package"></a>若要將父封裝組態加入子封裝  
  
1.  如果子封裝尚未開啟，請在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中開啟它。  
  
2.  按一下 [控制流程]**** 索引標籤之設計介面中的任意位置。  
  
3.  在 [SSIS]  功能表上，按一下 [封裝組態]  。  
  
4.  在 [封裝組態組合管理]**** 對話方塊中，選取 [啟用封裝組態]****，然後按一下 [加入]****。  
  
5.  在 [套件設定向導] 的 [歡迎使用] 頁面上，按 **[下一步]。**  
  
6.  在 [選取組態類型] 頁面的 [組態類型]**** 清單中，選取 [父封裝變數]****，然後執行下列其中之一：  
  
    -   選取 [直接指定組態設定]****，然後在 [父變數]**** 方塊中，提供組態中所要使用之父封裝的變數名稱。  
  
        > [!IMPORTANT]  
        >  變數名稱會區分大小寫。  
  
    -   選取 [組態位置儲存在環境變數中]****，然後在 [環境變數清單]**** 中選取包含變數名稱的環境變數。  
  
7.  按 [下一步]  。  
  
8.  在 [選取目標屬性] 頁面上，依序展開 [變數]**** 節點及要設定之變數的 [屬性]**** 節點，然後按一下組態所要設定的屬性。  
  
9. 按 [下一步]  。  
  
10. (選擇性) 在 [正在完成精靈] 頁面上，修改組態的預設名稱並檢閱組態資訊。  
  
11. 按一下 [完成]**** 以完成精靈，並返回 [封裝組態組合管理]**** 對話方塊。  
  
12. 在 [封裝組態組合管理]**** 對話方塊中，[組態]**** 方塊會列出新的組態。  
  
13. 按一下 **關閉**。  
  
## <a name="see-also"></a>另請參閱  
 [套件設定](../../2014/integration-services/package-configurations.md)   
 [建立套件設定](../../2014/integration-services/create-package-configurations.md)   
 [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)   
 [在封裝中使用變數](../../2014/integration-services/use-variables-in-packages.md)  
  
  
