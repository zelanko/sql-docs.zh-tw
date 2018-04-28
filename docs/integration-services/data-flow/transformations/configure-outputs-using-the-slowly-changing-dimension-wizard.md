---
title: 使用緩時變維度精靈來設定輸出 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Slowly Changing Dimension transformation
- slowly changing dimensions
- Slowly Changing Dimension Wizard
ms.assetid: da111731-1ffa-49b9-bcaa-3c93fd0eb619
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 201a34950a0b819970a25509339d69d6143b0caf
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="configure-outputs-using-the-slowly-changing-dimension-wizard"></a>使用緩時變維度精靈來設定輸出
  「緩時變維度精靈」做為「緩時變維度」轉換的編輯器使用。 為緩時變維度資料建立並設定資料流程會是一個複雜的工作。 「緩時變維度精靈」可引導您執行對應資料行、選取商務索引鍵資料行、設定資料行變更屬性，以及設定對推斷之維度成員的支援等步驟，為「緩時變維度」轉換輸出提供建立資料流程的最簡單方法。  
  
 您必須在維度資料表中選取至少一個商務索引鍵資料行，並將其對應到輸入資料行。 商務索引鍵值會將來源中的記錄連結到維度資料表中的記錄。 轉換會使用這個對應尋找維度資料表中的記錄，並判斷記錄是新的還是變更的。 通常，商務索引鍵是來源中的主索引鍵，但只要它會唯一識別記錄且其值不變更，就可以是替代索引鍵。 商務索引鍵也可以是包含多個資料行的複合索引鍵。 維度資料表中的主索引鍵通常是代理索引鍵，表示由識別欄位或自訂方案 (例如指令碼) 自動產生的數值。  
  
 在可執行「緩時變維度精靈」之前，必須先將來源和「緩時變維度」轉換加入到資料流程，然後將來源的輸出連接到「緩時變維度」轉換的輸入。 (選擇性) 資料流程可以包含資料來源和「緩時變維度」轉換之間的其他轉換。  
  
 若要開啟 [ [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師] 中的 [緩時變維度精靈]，請按兩下「緩時變維度」轉換。  
  
## <a name="creating-slowly-changing-dimension-outputs"></a>建立緩時變維度輸出  
  
#### <a name="to-create-slowly-changing-dimension-transformation-outputs"></a>若要建立緩時變維度轉換輸出  
  
1.  選擇連接管理員，以存取包含您要更新之維度資料表的資料來源。  
  
     您可以從封裝包含的連接管理員清單中選取。  
  
2.  選取您要更新的維度資料表或檢視。  
  
     選取連接管理員後，可以從資料來源選取資料表或檢視。  
  
3.  在資料行上設定索引鍵屬性，並將輸入資料行對應到維度資料表中的資料行。  
  
     您必須在維度資料表中選取至少一個商務索引鍵資料行，並將其對應到輸入資料行。 其他輸入資料行可以做為非索引鍵對應，對應到維度資料表中的資料行。  
  
4.  為每個資料行選取變更類型。  
  
    -   [變更屬性] 會覆寫記錄中的現有值。  
  
    -   [歷程記錄屬性] 會新建記錄而不是更新現有的記錄。  
  
    -   [固定屬性] 指示資料行的值不得變更。  
  
5.  設定固定和變更屬性選項。  
  
     如果設定資料行使用 [固定屬性] 變更類型，您可以指定在這些資料行中偵測到變更時，「緩時變維度」轉換是否失敗。 如果設定資料行使用 [變更屬性] 變更類型，則可以指定是否更新所有符合的記錄，包括過期記錄。  
  
6.  設定記錄屬性選項。  
  
     如果設定資料行使用 [歷程記錄屬性] 變更類型，您必須選擇如何區分目前記錄和過期記錄。 您可以使用目前資料列指標資料行或兩個日期資料行，以識別目前資料列和過期資料列。 如果使用目前資料列指標資料行，可以將其設定為 **Current**、 **True** ，和 **Expired,** 或 **False** 。 您也可以輸入自訂值。 如果您使用兩個日期資料行，即開始日期和結束日期，則當透過輸入日期或選取系統變數然後使用其值的方式設定日期資料行值時，您可以指定要使用的日期。  
  
7.  指定對推斷成員的支援，並選擇推斷成員記錄包含的資料行。  
  
     將量值載入到事實資料表時，您可以為尚不存在的推斷成員建立最低記錄。 稍後，當有意義的資料可用時，可以更新維度記錄。 可以建立下列類型的最低記錄：  
  
    -   其所包含的所有變更類型之資料行均為 Null 的記錄。  
  
    -   其所包含的布林資料行指示該記錄為推斷成員的記錄。  
  
8.  檢閱「緩時變維度精靈」建立的組態。 視所支援的變更類型而定，可以將不同的資料流程元件組加入到封裝中。  
  
     下圖顯示一個資料流程範例，它支援固定屬性、變更屬性和記錄屬性變更、推斷的成員以及對符合記錄的變更。  
  
     ![來自緩時變維度精靈的資料流程](../../../integration-services/data-flow/transformations/media/dimensionwizard.gif "來自緩時變維度精靈的資料流程")  
  
## <a name="updating-slowly-changing-dimension-outputs"></a>更新緩時變維度輸出  
 更新「緩時變維度」轉換輸出之組態的最簡單方法，就是重新執行「緩時變維度精靈」並修改精靈頁面中的屬性。 您還可以使用 [進階編輯器] 對話方塊或以程式設計方式更新「緩時變維度」轉換。  
  
## <a name="see-also"></a>另請參閱  
 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
  
  
