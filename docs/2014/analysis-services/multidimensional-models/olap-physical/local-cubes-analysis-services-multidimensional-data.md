---
title: 本機 Cube (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], local
ms.assetid: e52e1515-35a7-4dc3-9bbf-736d176ba0c7
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3cc1e27115d898cc2ba839fb14d2f7edfa8c560f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37149279"
---
# <a name="local-cubes-analysis-services---multidimensional-data"></a>本機 Cube (Analysis Services - 多維度資料)
  若要建立、更新或刪除本機 Cube，您必須撰寫及執行 ASSL 指令碼或 AMO 程式。  
  
 本機 Cube 和本機採礦模型可讓用戶端工作站與網路中斷連接時，仍能進行分析。 例如，用戶端應用程式可能會呼叫 OLE DB for OLAP 9.0 Provider (MSOLAP.3)，以便載入本機 Cube 引擎來建立及查詢本機 Cube，如下圖所示：  
  
 ![本機 cube 和模型的用戶端架構](../../../analysis-services/dev-guide/media/as-localcubearch9.gif "本機 cube 和模型的用戶端架構")  
  
 與本機 Cube 進行互動時，ADMOD.NET 和分析管理物件 (AMO) 也會載入本機 Cube 引擎。 只有單一處理序可以存取本機 Cube 檔案，因為當本機 Cube 引擎建立本機 Cube 的連接時，它就會以獨佔方式鎖定本機 Cube 檔案。 透過處理序，最多允許五個同時連接。  
  
 .cub 檔可能會包含一個以上的 Cube 或資料採礦模型。 本機 Cube 和資料採礦模型的查詢由本機 Cube 引擎處理，不需要連接到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體。  
  
> [!NOTE]  
>  目前不支援使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 來管理本機 Cube。  
  
## <a name="local-cubes"></a>本機 Cube  
 可以建立本機 cube，並從現有 cube 中填入[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體或關聯式資料來源。  
  
|本機 Cube 的資料來源|建立方法|  
|------------------------------------|---------------------|  
|以伺服器為基礎的 Cube|您可以使用 CREATE GLOBAL CUBE 陳述式或[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]指令碼語言 (ASSL) 指令碼建立和擴展 cube 以伺服器為基礎的 cube。 如需詳細資訊，請參閱 <<c0> [ 建立 GLOBAL CUBE 陳述式&#40;MDX&#41; ](/sql/mdx/mdx-data-definition-create-global-cube)或是[Analysis Services Scripting Language &#40;ASSL&#41;參考](../../scripting/analysis-services-scripting-language-assl-for-xmla.md)。</c0>|  
|關聯式資料來源|您可以使用 ASSL 指令碼，根據 OLE DB 關聯式資料庫建立和擴展 Cube。 若要使用 ASSL 來建立本機 Cube，您只要連接至本機 Cube 檔案 (*.cub) 並以針對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體執行 ASSL 指令碼來建立伺服器 Cube 的相同方式執行 ASSL 指令碼即可。 如需詳細資訊，請參閱 < [Analysis Services Scripting Language &#40;ASSL&#41;參考](../../scripting/analysis-services-scripting-language-assl-for-xmla.md)。|  
  
 您可以使用 REFRESH CUBE 陳述式來重建本機 Cube 並更新其資料。 如需詳細資訊，請參閱 <<c0> [ 重新整理 CUBE 陳述式&#40;MDX&#41;](/sql/mdx/mdx-data-definition-refresh-cube)。</c0>  
  
### <a name="local-cubes-created-from-server-based-cubes"></a>根據以伺服器為基礎的 Cube 建立本機 Cube  
 根據以伺服器為基礎的 Cube 建立本機 Cube 時，請考量以下事項：  
  
-   不支援相異計數量值。  
  
-   當您加入量值時，至少必須同時加入一個與所加入之量值相關的維度。 如需有關量值群組的維度關聯性的詳細資訊，請參閱[維度關聯性](../../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)。  
  
-   當您加入父子式階層時，就會忽略父子式階層上的層級和篩選，而加入整個父子式階層。  
  
-   不會建立成員屬性。  
  
-   當您加入局部加總量值時，「帳戶」或「時間」維度上不允許使用任何配量。  
  
-   參考維度一定會具體化。  
  
-   包含多對多維度時，適用下列規則：  
  
    -   您無法配量多對多維度。  
  
    -   您必須從中繼量值群組加入量值。  
  
    -   您無法配量多對多關聯性中所涉及之兩個量值群組所共用的任何維度。  
  
-   只有依賴加入至本機 Cube 之量值與維度的這些導出成員、命名集和指派會顯示在本機 Cube 中。 系統將自動排除無效的導出成員、命名集和指派。  
  
### <a name="security"></a>Security  
 為了讓使用者從伺服器 cube 建立本機 cube，必須授與使用者**鑽研和本機 Cube**伺服器 cube 的權限。 如需詳細資訊，請參閱 <<c0> [ 授與 cube 或模型權限&#40;Analysis Services&#41;](../../multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)。</c0>  
  
 使用伺服器 Cube 等角色時，本機 Cube 不會受到保護。 擁有本機 Cube 檔案之檔案層級存取權的任何人都可以查詢其中的 Cube。 您可以使用本機 Cube 檔案的 `Encryption Password` 連接屬性來設定本機 Cube 檔案的密碼。 如果設定本機 Cube 檔案的密碼，就會要求本機 Cube 檔案的所有未來連接都要使用此密碼，才能查詢檔案。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE GLOBAL CUBE 陳述式&#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube)   
 [使用 Analysis Services 開發的指令碼語言&#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [重新整理 CUBE 陳述式&#40;MDX&#41;](/sql/mdx/mdx-data-definition-refresh-cube)  
  
  
