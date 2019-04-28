---
title: 複製採礦模型的檢視 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clipboards [data mining]
- Mining Model Viewer [Analysis Services], clipboards
- copying mining models to clipboard
ms.assetid: 768372db-e5b4-4990-b459-03d854fd9a6d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 62d699d068832e1b3e264a9346d03553b9a05d80
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62715265"
---
# <a name="copy-a-view-of-a-mining-model"></a>複製採礦模型的檢視
  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，資料採礦設計師的 [採礦模型檢視器] 索引標籤，對每一種類型的採礦模型都會使用個別的檢視器。 有幾個檢視器含有一些元件，您可將其內容複製至剪貼簿，再將剪貼簿內容複製到文件或影像操作軟體。 下列元件可以使用此功能：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集檢視器和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集檢視器中的群集圖表  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 樹狀檢視器和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列檢視器中的決策樹  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集檢視器中的狀態轉換  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯規則檢視器、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類檢視器和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 樹狀檢視器中的相依性網路  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般內容樹狀檢視器之 [節點詳細資料] 窗格中的採礦模型內容  
  
 您可以複製完整的採礦模型表示，或只複製檢視器可見的部分。  
  
> [!WARNING]  
>  當您使用檢視器複製模型時，不會建立新的模型物件。 若要建立新模型，您必須使用精靈或資料採礦設計師。 如需詳細資訊，請參閱 [建立採礦模型的複本](make-a-copy-of-a-mining-model.md)。  
  
### <a name="to-copy-the-complete-model-to-the-clipboard"></a>將完整的模型複製到剪貼簿  
  
1.  從 [採礦模型檢視器] 索引標籤的 [採礦模型] 清單中，選取您要檢視的採礦模型。  
  
2.  選取適當的索引標籤，例如 [相依性網路] 索引標籤，然後按一下該索引標籤之工具列上的 [複製整個圖表]。  
  
### <a name="to-copy-the-visible-piece-of-the-model-to-the-clipboard"></a>若要將模型的可見部份複製到剪貼簿  
  
1.  從 [採礦模型檢視器] 索引標籤的 [採礦模型] 清單中，選取您要檢視的採礦模型。  
  
2.  選取適合的索引標籤，例如 [相依性網路] 索引標籤，然後放大或縮小，在您要的層級上檢視模型。  
  
3.  按一下所選取索引標籤之工具列上的 [複製圖表檢視]。  
  
### <a name="to-copy-the-mining-model-content-to-the-clipboard"></a>將採礦模型內容複製到剪貼簿  
  
1.  從 [採礦模型檢視器] 索引標籤的 [採礦模型] 清單中，選取您要檢視的採礦模型。  
  
2.  從 [檢視器] 下拉式清單中，選取 [Microsoft 一般內容樹狀檢視器]。  
  
3.  在 [節點標題 (唯一 ID)] 窗格中，按一下節點。  
  
4.  以滑鼠右鍵按一下 [節點詳細資料] 窗格，然後選取 [全選]。  
  
5.  再次以滑鼠右鍵按一下 [節點詳細資料] 窗格，然後選取 [複製]。  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型檢視器工作和操作說明](mining-model-viewer-tasks-and-how-tos.md)  
  
  
