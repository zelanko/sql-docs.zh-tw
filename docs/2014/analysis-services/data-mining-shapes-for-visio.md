---
title: 適用于 Visio 的資料採礦圖形 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining shapes
- templates [Visio]
- Visio shapes
- shapes, data mining
ms.assetid: 11a821d9-1c0a-442e-b735-92208ce479dc
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1d30456ac3685aa3dc40af6f1c79f92796fc1404
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84525774"
---
# <a name="data-mining-shapes-for-visio"></a>適用於 Visio 的資料採礦圖形
  適用於 Visio 的資料採礦圖形提供了針對顯示資料採礦模型所自訂的範本。 使用這些範本就能連接到您已建立的模型，也可建立互動式簡報以說明資料採礦的結果。  
  
 範本提供了許多優於靜態圖形和螢幕擷取畫面的優點-它們會與基礎資料採礦模型互動，這些模型儲存在 Analysis Services 的實例上，並可讓您自訂顯示模型中模式的方式。 您可以摺疊和展開樹狀模型、依資料節點或屬性進行篩選，以及顯示模型統計資料 (例如機率和係數)。  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Visio 範本包含下列精靈：  
  
-   相依性**網狀圖表：** 使用此 wizard 建立決策樹和類神經網路的圖形。  
  
-   **決策樹圖表：** 使用此 wizard 建立圖表，以顯示與決策樹模型相關聯的決策點和公式。 這類圖表也可以搭配迴歸模型使用。  
  
-   **群集圖表：** 使用此嚮導為您的分割模型建立彩色圖形。 您可以在各種檢視 (例如屬性辨識、叢集設定檔與相依性) 之間切換，以及自訂叢集的外觀。  
  
## <a name="installation"></a>安裝  
 當您安裝適用于 Visio 的資料採礦範本時，根據預設，下列檔案會安裝到 \<drive> \Program Files\Microsoft SQL Server 2012 DM 增益集（或 \<drive> \ 或 Program files （x86） \Microsoft SQL SERVER 2012 DM 增益集）：  
  
-   **Microsoft 資料發掘**此範本包含預先設計的格式設定、配置和嚮導，可協助您使用資料採礦圖形。  
  
-   **Microsoft 資料採礦圖形 Studio .vss**此樣板檔案包含與範本相關聯的圖形。  
  
## <a name="how-to-use-the-templates"></a>如何使用範本  
 若要開啟範本，您可以按兩下圖形檔，也可以開啟 Visio 然後再開啟圖形範本。  
  
1.  從樣板將其中一個 Visio 資料採礦圖形置於新頁面上。  
  
2.  精靈啟動時，請連接到存有您想要顯示之資料採礦模型的伺服器。  
  
3.  選取資料採礦模型，讓模型類型符合視覺化類型。  
  
4.  設定應該要如何顯示及格式化資料的選項。  
  
5.  當您完成「**資料採礦圖形」 Wizard**之後，您就可以使用 Visio 的功能來修改和增強圖表。  
  
 如需如何使用和增強 Visio 模型圖表的詳細資訊，請參閱[在 visio 中觀看資料採礦模型 &#40;資料採礦增益集&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)  
  
## <a name="requirements"></a>規格需求  
  
-   若要使用範本，您必須先建立與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。  
  
     精靈會提示您選取 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器及指定包含採礦模型的資料庫。  
  
     如需有關如何建立連線的詳細資訊，請參閱[連接到來源資料 &#40;適用于 Excel&#41;的資料採礦用戶端](connect-to-source-data-data-mining-client-for-excel.md)。  
  
-   如果您使用資料表分析工具，請務必將模型儲存至 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器，切勿使用暫時性模型。  
  
-   模型必須已使用其中一種支援的演算法建立：群集、決策樹、類神經網路、貝氏機率分類或羅吉斯迴歸。  
  
  
