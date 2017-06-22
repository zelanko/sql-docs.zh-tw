---
title: "建立關聯式查詢設計工具 （報表產生器及 SSRS） 中的查詢 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 28b25861-f3b4-4c3e-a9b0-03d6e4cfea26
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8f7c711b3cd56302b05d7dcf4f3045283c376d73
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="build-a-query-in-the-relational-query-designer-report-builder-and-ssrs"></a>在關聯式查詢設計工具中建立查詢 (報表產生器及 SSRS)
  查詢設計工具可協助您針對報表資料集，指定要從外部資料來源擷取的資料。 當您在精靈中建置查詢或建立資料集查詢時，就會使用查詢設計工具。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 資料集是以資料來源為基礎。 資料來源的類型以及撰寫環境會決定當您定義資料集查詢時開啟的查詢設計工具。 查詢設計工具功能會因基礎資料來源而異。 如需資料層級的詳細資訊，請參閱[報表產生器中的資料連接、資料來源及連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)或[資料連接、資料來源及連接字串 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
  
 您可以使用查詢設計工具進行下列工作：  
  
-   瀏覽外部資料來源上多個結構描述的中繼資料  
  
-   指定要為資料集擷取的欄位  
  
-   指定兩個物件 (如資料表) 之間的關聯性  
  
-   指定篩選條件來限制擷取的報表資料  
  
-   指出是否要建立參數  
  
-   指定要在外部資料來源上執行計算的彙總  
  
 開啟查詢設計工具後，不論是內嵌資料集或共用資料集，建立查詢的方式均相同。 下列程序使用內嵌資料集查詢。  
  
 如需詳細資訊，請參閱[關聯式查詢設計工具使用者介面 &#40;報表產生器&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md)。  
  
### <a name="to-build-a-query-for-an-embedded-dataset-in-report-design-view"></a>若要在報表設計檢視中建立內嵌資料集的查詢  
  
1.  開啟查詢設計工具。 在 [報表資料] 窗格中，以滑鼠右鍵按一下此資料集，然後按一下 [查詢]。  
  
     隨即開啟與資料來源相關聯的查詢設計工具。  
  
2.  在 [資料庫檢視] 窗格中，展開資料夾，顯示資料庫結構描述物件 (如資料表、檢視表和預存程序) 的階層式檢視。 按一下選取方塊來選取物件的所有欄位，或展開節點來選取個別欄位。  
  
     當您從 [資料庫檢視] 窗格選取欄位時， **[選取欄位]** 窗格會顯示您選取的項目。  
  
     如果您從一個以上的關聯資料庫資料表選取欄位，請使用 [關聯性] 窗格檢視從資料庫結構描述偵測到的資料表關聯性。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     資料集欄位清單會出現在 [報表資料] 窗格中。  
  
### <a name="to-specify-limits-for-a-query"></a>若要指定查詢的限制條件  
  
1.  在關聯式查詢設計工具中，確認您已選取欄位，且欄位出現在 **[選取的欄位]** 窗格中。  
  
2.  在 [套用的篩選器] 窗格工具列中，按一下 **[加入篩選]**。 新的篩選資料列隨即顯示。  
  
3.  在 [欄位名稱] 中，按一下以顯示欄位的下拉式清單，然後按一下篩選所要依據的欄位名稱。 例如，若要依數量篩選，請按一下包含項目數的欄位。  
  
4.  在 [運算子] 中，按一下以顯示運算子的下拉式清單，然後選取要用於篩選的比較運算子。  
  
5.  在 **[值]**中，輸入篩選所要依據的值。 例如，若要篩選出超過 100 的數量，請輸入 100。  
  
6.  在此資料列中選取參數選項來建立資料集參數，以便讓使用者指定篩選值。 系統會自動建立符合資料集參數的報表參數。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 資料集欄位清單會出現在 [報表資料] 窗格中。  
  
### <a name="to-view-a-query-result-set"></a>若要檢視查詢結果集  
  
1.  在查詢設計工具工具列上，按一下 [執行查詢] (!)。  
  
    > [!NOTE]  
    >  查詢設計工具會使用設計階段認證執行查詢和擷取結果集。 如需詳細資訊，請參閱 [在報表產生器中指定認證](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
 查詢會在資料來源上執行，並將範例資料傳回 [查詢結果] 窗格。  
  
## <a name="see-also"></a>請參閱＜  
 [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [從外部資料來源加入資料 &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)   
 [查詢設計工具 &#40;報表產生器&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)   
 [建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [報表設計檢視 &#40;報表產生器&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [共用資料集設計檢視 &#40;報表產生器&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
 [Reporting Services 查詢設計工具](http://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835)  
  
  
