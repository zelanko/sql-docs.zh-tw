---
title: "將帳戶智慧加入維度 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], account intelligence
- account intelligence [Analysis Services]
ms.assetid: 36f454ae-a9f2-4a59-b19d-40310af9f901
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 970daabf89244a93719e273b4bff7f322cb23fe6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="bi-wizard---add-account-intelligence-to-a-dimension"></a>BI 精靈-將帳戶智慧加入維度中
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]將帳戶智慧增強功能加入至 cube 或維度以將標準科目分類，例如收入與費用，指派給帳戶屬性的成員。 此增強功能也會識別科目類型 (例如資產和負債)，並對每一個科目類型指派適當的彙總。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可使用分類隨時間彙總科目。  
  
> [!NOTE]  
>  只有以現有的資料來源為基礎的維度才可使用帳戶智慧。 對於沒有使用資料來源建立的維度，在加入帳戶智慧之前，您必須執行結構描述產生精靈來建立資料來源檢視。  
  
 您可以將帳戶智慧套用至指定帳戶資訊的維度 (例如，帳戶名稱、帳戶號碼和帳戶類型)。 若要加入帳戶智慧，您可以使用商業智慧精靈，並選取 **[選擇增強功能]** 頁面上的 **[定義帳戶智慧]** 選項。 此精靈就會引導您完成一些步驟，來選取您要套用帳戶智慧的維度、在選取的帳戶維度中識別帳戶屬性，然後將維度資料表中的帳戶類型對應到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]所辨識的帳戶類型。  
  
## <a name="selecting-a-dimension"></a>選取維度  
 在精靈的第一個 **[定義帳戶智慧]** 頁面上，您可以指定要套用帳戶智慧的維度。 帳戶智慧增強功能加入這個選取的維度之後，會導致維度變更。 包含選取之維度的所有 Cube，都會繼承這些變更。  
  
## <a name="specifying-account-attributes"></a>指定帳戶屬性  
 在精靈的 **[設定維度屬性]** 頁面上，您可以指定已選取之帳戶維度中的帳戶屬性。 首先，在 **[包含]** 資料行中，選取您要對應到維度中之維度資料表每一個帳戶屬性類型旁邊的核取方塊。 然後，在 [維度屬性] 資料行中，展開下拉式清單，並在維度中選取對應到所選取之屬性類型的屬性。 從清單中選取屬性，會設定帳戶屬性的 **Type** 屬性。  
  
## <a name="mapping-account-types"></a>對應帳戶類型  
 第二個 **[定義帳戶智慧]** 頁面將維度資料表中的帳戶類型值，對應到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]所辨識的帳戶類型。 唯有當您在維度中包含 **[帳戶類型]** 維度屬性時，這個頁面才會出現。 若要包含 **[帳戶類型]** 維度，請在精靈的 **[定義帳戶智慧設定]** 頁面上，選取 **[帳戶類型]**旁邊的核取方塊，然後選取適當的屬性。  
  
 在第二個 **[定義帳戶智慧]** 頁面上，有兩個資料行：  
  
-   **[來源資料表帳戶類型]** 資料行列出精靈從維度資料表取得的帳戶類型。  
  
-   **[伺服器帳戶類型]** 資料行會識別 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所辨識的對應帳戶類型。 下表列出 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所辨識的帳戶類型，以及每一個這些類型的預設彙總。 如果維度資料表使用的帳戶類型名稱與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用的一樣，則會自動選取。  
  
    |伺服器帳戶類型|彙總|描述|  
    |-------------------------|-----------------|-----------------|  
    |**統計**|**無**|某項目的計算比率，或者經過一段時間無法彙總之項目的計數。 此帳戶類型不使用轉換規則來轉換貨幣。|  
    |**負債**|**LastNonEmpty**|在特定時間虧欠之事物的金額或價值。 此帳戶類型經過一段時間不會累積，因此經過一段時間不會自然彙總。 例如，Year 數量是有資料的上一個月的值。 這種類型的帳戶會以 End of Period 匯率轉換貨幣。|  
    |**資產**|**LastNonEmpty**|在特定時間持有之事物的金額或價值。 此帳戶類型經過一段時間會累積，因此不會隨著時間自然彙總。 例如，Year 數量是有資料的上一個月的值。 這種類型的帳戶會以 End of Period 匯率轉換貨幣。|  
    |**結餘**|**LastNonEmpty**|某項目在指定之時間的計數。 此帳戶類型會累積，但不會隨著時間自然彙總。 例如，Year 數量是有資料的上一個月的值。|  
    |**流量**|**Sum**|某項目的累加計數。 此帳戶類型經過一段時間會彙總成為 **Sum** ，但不會以貨幣轉換規則轉換。|  
    |**費用**|**Sum**|所花費之事物的金額或價值。 這種帳戶類型會隨時間彙總為 **Sum** ，並以平均匯率轉換貨幣。|  
    |**Income**|**Sum**|所收到之事物的金額或價值。 這種帳戶類型會隨時間彙總為 **Sum** ，並以平均匯率轉換貨幣。|  
  
    > [!NOTE]  
    >  適合的話，您可以將維度中一個以上的帳戶類型，對應到特定伺服器帳戶類型。  
  
 若要變更已對應到資料庫之每一個帳戶類型的預設彙總，您可以使用資料庫設計工具。  
  
1.  在方案總管中，以滑鼠右鍵按一下 Analysis Services 專案，然後按一下 [編輯資料庫]。  
  
2.  在 **[帳戶類型對應]** 方塊中，於 **[名稱]**中選取帳戶類型。  
  
3.  在 **[別名]** 文字方塊中，輸入此帳戶類型的別名。  
  
4.  在 **[彙總函式]** 下拉式清單方塊中，變更這個帳戶類型的預設彙總函式。  
  
  
