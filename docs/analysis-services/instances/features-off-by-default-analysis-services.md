---
title: "根據預設 (Analysis Services) 功能關閉 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a9529edf-337e-4fdd-9a13-99cfe96b4fa1
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 21ff5e0b59b3e14df550bb580b1c59dde449452e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="features-off-by-default-analysis-services"></a>預設關閉的功能 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]執行個體[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]預設為安全保護。 因此，依預設會停用有可能危及安全性的功能。 下列功能會以停用狀態安裝，如果您想要使用這些功能，必須特地加以啟用：  
  
## <a name="feature-list"></a>功能清單  
 若要啟用下列功能，請使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接至 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 以滑鼠右鍵按一下執行個體名稱，然後選擇 [Facet]。 或者，可利用下節中所述的伺服器屬性，啟用這些功能。  
  
-   特定資料採礦 (OpenRowset) 查詢  
  
-   連結物件 (To)  
  
-   連結物件 (From)  
  
-   只接聽本機連接  
  
-   使用者定義的函式  
  
## <a name="server-properties"></a>伺服器屬性  
 其他依預設關閉的功能，均可透過伺服器屬性加以啟用。 使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 以滑鼠右鍵按一下執行個體名稱，然後選擇 [屬性]。 按一下 [一般] ，然後按一下 [顯示進階]  即可顯示更大的屬性清單。  
  
-   特定資料採礦 (OpenRowset) 查詢  
  
-   允許工作階段採礦模型 (資料採礦)  
  
-   連結物件 (To)  
  
-   連結物件 (From)  
  
-   以 COM 為基礎的使用者定義函式  
  
-   飛行記錄器追蹤定義 (範本)。  
  
-   查詢記錄  
  
-   只接聽本機連接  
  
-   二進位 XML  
  
-   壓縮  
  
-   群組相似性。 如需詳細資訊，請參閱＜ [Thread Pool Properties](../../analysis-services/server-properties/thread-pool-properties.md) ＞。  
  
  
