---
title: 自訂報表中的參數窗格 (報表產生器) | Microsoft Docs
description: 了解如何在報表產生器中使用參數建立編頁報表時，自訂 [參數] 窗格。
ms.date: 06/15/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4ce9e8d5-911a-4422-928f-a8d005b79fc6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 29bd397d64280644394077a29a3420dbf43b5e6f
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796559"
---
# <a name="customize-the-parameters-pane-in-a-report-report-builder"></a>Customize the Parameters Pane in a Report (Report Builder)
  在報表產生器中使用參數來建立分頁報表時，您可以自訂 [參數] 窗格。 在報表設計檢視中，您可以將參數拖曳到 [參數] 窗格中的特定資料行和資料列。 您可以新增及移除資料行以變更窗格配置。

 當您在窗格中將參數拖曳至新的資料行和資料列時，參數順序會在 [報表資料] 窗格中變更。 當您在 [報表資料] 窗格中變更參數的順序時，參數在窗格中的位置會變更。 如需參數順序為何重要的詳細資訊，請參閱[變更報表參數的順序 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)。

## <a name="to-customize-the-parameters-pane"></a>自訂參數窗格

1.  在 [檢視]  索引標籤上，選取 [參數]  核取方塊以顯示參數窗格。

     ![從 [檢視] 索引標籤存取 [參數] 窗格](../../reporting-services/report-design/media/ssrs-customparameter-accessparameterpanedesignmode.png "從 [檢視] 索引標籤存取 [參數] 窗格")

     窗格會出現在設計介面的頂端。

2.  若要將參數加入窗格中，請執行下列其中一項。

    -   在參數窗格中以滑鼠右鍵按一下空的資料格，然後按一下 [加入參數] 。

         ![從 [參數] 窗格新增參數](../../reporting-services/report-design/media/ssrs-customizeparameter-addnewparameter.png "從 [參數] 窗格新增參數")

    -   在 [報表資料] 窗格中以滑鼠右鍵按一下 [參數]，然後按一下 [加入參數]。

3.  若要將參數移到參數窗格中的新位置，請將參數拖曳到窗格中的不同資料格。

     當您在窗格中變更參數的位置時，[報表資料] **** 窗格中，參數在 [參數] **** 清單中的順序會自動變更。 如需參數順序影響的詳細資訊，請參閱[變更報表參數的順序 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)

4.  若要存取參數的屬性，請執行下列其中一項動作。

    -   在參數窗格中，以滑鼠右鍵按一下參數，然後按一下 [參數屬性] 。

         ![從 [參數] 窗格存取參數屬性](../../reporting-services/report-design/media/ssrs-customizeparameter-accessparameterproperties-composite.png "從 [參數] 窗格存取參數屬性")

    -   在 [報表資料] 窗格中，以滑鼠右鍵按一下參數 ，然後按一下 [參數屬性]。

5.  若要將新的資料行和資料列加入窗格中，或刪除現有的資料列和資料行，請以滑鼠右鍵按一下參數窗格中的任何位置，然後在顯示的功能表上按一下命令。

     ![將資料行和資料列新增至 [參數] 窗格](../../reporting-services/report-design/media/ssrs-customparameter-addcolumnsrows.png "將資料行和資料列新增至 [參數] 窗格")

    > [!IMPORTANT]
    >  當您刪除包含參數的資料行或資料列時，參數會從報表中刪除。

6.  若要從窗格以及從報表刪除參數，請執行下列其中一項動作。

    -   在參數窗格中，以滑鼠右鍵按一下參數，然後按一下 [刪除]  。

         ![從 [參數] 窗格刪除參數](../../reporting-services/report-design/media/ssrs-customparameter-deleteparameter.png "從 [參數] 窗格刪除參數")

    -   在 [報表資料] 窗格中，以滑鼠右鍵按一下參數，然後按一下 [刪除]。

## <a name="hiddeninternal-parameters-during-runtime"></a>執行階段期間的隱藏/內部參數
如果具有隱藏/內部參數，則在執行階段期間是否會將其轉譯為空白空間的邏輯如下所示：

   - 如果任何資料列或資料行只包含隱藏/內部參數或空白資料格，則在執行階段期間不會轉譯整個資料列或資料行
   - 否則，隱藏/內部參數或空白資料格將會轉譯為空白空間

例如，`ReportParameter1` 會隱藏，而其餘的參數則為可見：

![隱藏參數範例 1](../../reporting-services/report-design/media/ssrs-hidden-parameter-rb-1.png "配置方格中的一個隱藏參數")

這會在執行階段期間產生空白空間，因為第一個資料行或第一個資料列中有可見參數：

![隱藏參數範例 1 - 執行階段](../../reporting-services/report-design/media/ssrs-hidden-parameter-server-1.png "配置方格內其中一個隱藏參數導致執行階段中的空白空間")

使用相同的範例 (如果也將 `ReportParameter3` 設定為隱藏的話)：

![隱藏參數範例 2](../../reporting-services/report-design/media/ssrs-hidden-parameter-rb-2.png "相同資料行中的兩個隱藏參數")

然後，在執行階段期間不會轉譯第一個資料行，因為會將整個資料行視為空白：

![隱藏參數範例 2 - 執行階段](../../reporting-services/report-design/media/ssrs-hidden-parameter-server-2.png "執行階段內相同資料行中的兩個隱藏參數")

## <a name="default-layout"></a>預設配置
針對在 SQL Server Reporting Services 2016 之前撰寫的報表，在執行階段期間會使用 2 個資料行和 N 個資料列的預設參數配置方格。 若要變更預設配置，請在 Microsoft 報表產生器中開啟報表，然後儲存報表。 儲存報表之後，自訂的參數配置資訊將會儲存至 .rdl 檔案。


## <a name="see-also"></a>另請參閱
 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)


