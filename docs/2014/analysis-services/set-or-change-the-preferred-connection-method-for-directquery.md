---
title: 設定或變更 DirectQuery 的慣用的連接方法 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f10d5678-d678-4251-8cce-4e30cfe15751
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9737b829a5ccab1ddc0362f2d8ac81285f0f6e1c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068703"
---
# <a name="set-or-change-the-preferred-connection-method-for-directquery"></a>設定或變更 DirectQuery 的慣用連接方法
  當您建立要用於 DirectQuery 模式的模型時，必須先將設計環境設定為支援使用 DirectQuery。 若要這樣做，請參閱[啟用 DirectQuery 設計模式&#40;SSAS 表格式&#41;](tabular-models/enable-directquery-mode-in-ssdt.md)。  
  
 在您準備部署模型時，必須設定其他屬性，讓使用者能夠以其中一種 DirectQuery 模式來存取您的模型：  
  
-   您必須指示對模型的查詢應該使用快取資料還是關聯式資料來源。 您可以使用混合模式或僅限 DirectQuery 模式。  
  
-   如果您使用資料分割，則必須指定哪個資料分割要做為 DirectQuery 資料來源。  
  
-   您必須為將存取 SQL Server 資料來源的使用者設定模擬選項。  
  
 此程序描述如何在設計工具中為 DirectQuery 模型設定慣用連接方法。 此外也描述如何在部署模型後於 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 變更此屬性。  
  
### <a name="to-set-the-preferred-connection-method-for-a-directquery-model"></a>若要為 DirectQuery 模型設定慣用連接方法  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟 DirectQuery 模型的方案檔。  
  
2.  在 Visual Studio 中，選取 **[專案]** 功能表中的 **[屬性]** 。  
  
3.  在 **[屬性]** 窗格中，將屬性 **DirectQueryMode**變更為支援 DirectQuery 使用的下列其中一個值：  
  
    -   **Inmemorywithdirectquery**:如果您使用此選項時，將模型部署，但您可以對模型執行查詢之前，您必須處理快取。  
  
    -   **搭配使用 DirectQuery 和 InMemory**:如果您使用此選項時，快取可供使用的用戶端已處理。 如果以此設定來部署模型但未處理快取，則某些用戶端在嘗試連接至模型時勢必會收到錯誤訊息。  
  
    -   **僅限 DirectQuery**:如果您使用此選項時，會部署中繼資料，但模型中沒有任何資料。 嘗試使用記憶體中模式進行連接的用戶端將會收到錯誤訊息，指出模型不存在或尚未處理。  
  
4.  如果發生錯誤，請在 Visual Studio 中開啟 **[錯誤清單]** ，並且解決阻礙模型以 DirectQuery 模式部署的任何問題。  
  
### <a name="to-verify-or-change-the-preferred-connection-method-for-a-directquery-model"></a>若要為 DirectQuery 模型驗證或變更慣用連接方法  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中，連接至部署了 DirectQuery 模型的執行個體。  
  
2.  以滑鼠右鍵按一下模型資料庫，然後選取 **[屬性]** 。  
  
3.  在 **[屬性]** 窗格中，將屬性 **DirectQueryMode**變更為下列其中一個值：  
  
    -   **僅限 DirectQuery**  
  
    -   **InMemory 和 DirectQuery**  
  
    -   **搭配使用 DirectQuery 和 InMemory**  
  
 請注意，這些屬性與您在部署前於 Visual Studio 對專案設定的屬性相同。 只要您已將模型設定為支援使用 DirectQuery，隨時可以變更 DirectQuery 模式的慣用連接模式。  
  
## <a name="see-also"></a>另請參閱  
 [DirectQuery 模式 &#40;SSAS 表格式&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [啟用 DirectQuery 設計模式&#40;SSAS 表格式&#41;](tabular-models/enable-directquery-mode-in-ssdt.md)  
  
  
