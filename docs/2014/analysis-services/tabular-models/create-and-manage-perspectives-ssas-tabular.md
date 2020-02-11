---
title: 建立和管理觀點（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.perspectivedb.f1
ms.assetid: 2a411c2b-2820-4086-ad7f-ce6a941fefc7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b920446018c9199ed0bd436e67a65d43341f7f43
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067433"
---
# <a name="create-and-manage-perspectives-ssas-tabular"></a>建立及管理檢視方塊 (SSAS 表格式)
  檢視方塊會定義可檢視之模型子集，對模型提供具體的商務特有或應用程式特有視點。 本主題中的工作會描述如何使用模型設計師中的 **[檢視方塊]** 對話方塊，建立及管理檢視方塊。  
  
 本主題也包括下列工作：  
  
-   [若要加入觀點](#bkmk_add)  
  
-   [編輯觀點](#bkmk_edit)  
  
-   [若要重新命名觀點](#bkmk_rename)  
  
-   [若要刪除觀點](#bkmk_delete)  
  
-   [複製觀點](#bkmk_copy)  
  
## <a name="tasks"></a>工作  
 若要建立檢視方塊，請使用 **[檢視方塊]** 對話方塊，即可在其中加入、編輯、刪除、複製及查看檢視方塊。 若要在 **中檢視** [檢視方塊] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]對話方塊，請按一下 **[模型]** 功能表，然後按一下 **[檢視方塊]**。  
  
###  <a name="bkmk_add"></a>若要加入觀點  
  
-   若要加入新檢視方塊，請按一下 **[新增檢視方塊]**。 即可核取或取消核取要包含的欄位物件，並提供新檢視方塊的名稱。  
  
     如果您建立空白檢視方塊 (已取消核取所有欄位物件)，則使用此檢視方塊的使用者會看到空白的欄位清單。 檢視方塊應該至少包含一個資料表和一個資料行。  
  
###  <a name="bkmk_edit"></a>編輯觀點  
  
-   若要修改觀點，請檢查並取消核取觀點的資料行中的欄位，這會從觀點來加入和移除欄位物件。  
  
###  <a name="bkmk_rename"></a>若要重新命名觀點  
  
-   當您將滑鼠停留在觀點的資料行標頭（觀點的名稱）上方時，[**重新命名**] 按鈕隨即出現。 若要重新命名檢視方塊，請按一下 **[重新命名]**，然後輸入新名稱或編輯現有名稱。  
  
###  <a name="bkmk_delete"></a>若要刪除觀點  
  
-   當您將滑鼠停留在觀點的資料行標頭（觀點的名稱）上方時，就會出現 [**刪除**] 按鈕。 若要刪除檢視方塊，請按一下 **[刪除]** 按鈕，然後在確認視窗中按一下 **[是]** 。  
  
###  <a name="bkmk_copy"></a>複製觀點  
  
-   當您將滑鼠停留在某個觀點的資料行標頭上方時，[**複製**] 按鈕隨即出現。 若要複製檢視方塊，請按一下 **[複製]** 按鈕。 在現有檢視方塊的右邊就會加入選定檢視方塊的副本，做為新檢視方塊。 新檢視方塊會繼承原本檢視方塊的名稱，並且於名稱結尾處加上 *- 複本* 註記。 例如，如果建立了*銷售*觀點的副本，新的觀點就稱為「*銷售-複製*」。  
  
## <a name="see-also"></a>另請參閱  
 [SSAS 表格式 &#40;的觀點&#41;](perspectives-ssas-tabular.md)   
 [SSAS 表格式&#41;的階層 &#40;](hierarchies-ssas-tabular.md)  
  
  
