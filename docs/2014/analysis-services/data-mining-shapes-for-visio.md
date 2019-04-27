---
title: 適用於 Visio 的資料採礦圖形 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining shapes
- templates [Visio]
- Visio shapes
- shapes, data mining
ms.assetid: 11a821d9-1c0a-442e-b735-92208ce479dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92630f90d7b18ad668dcffc02feeb65990cf3c84
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62690004"
---
# <a name="data-mining-shapes-for-visio"></a>適用於 Visio 的資料採礦圖形
  適用於 Visio 的資料採礦圖形提供了針對顯示資料採礦模型所自訂的範本。 使用這些範本就能連接到您已建立的模型，也可建立互動式簡報以說明資料採礦的結果。  
  
 範本提供許多優於靜態圖形和螢幕擷取畫面-它們互動基礎的資料採礦模型，儲存在 Analysis Services 的執行個體，並可讓您自訂採礦模型中的模式的顯示方式。 您可以摺疊和展開樹狀模型、依資料節點或屬性進行篩選，以及顯示模型統計資料 (例如機率和係數)。  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Visio 範本包含下列精靈：  
  
-   **相依性網路圖表：** 您可以使用這個精靈來建立決策樹和類神經網路的圖形。  
  
-   **決策樹圖表：** 您可以使用這個精靈來建立圖表，顯示的決策點和決策樹模型相關聯的公式。 這類圖表也可以搭配迴歸模型使用。  
  
-   **叢集圖表：** 您可以使用此精靈來建立分割模型的彩色圖形。 您可以在各種檢視 (例如屬性辨識、叢集設定檔與相依性) 之間切換，以及自訂叢集的外觀。  
  
## <a name="installation"></a>安裝  
 當您安裝適用於 Visio 的資料採礦範本時，根據預設會安裝下列檔案到\<磁碟機 > files\microsoft SQL Server 2012 DM Add-ins (或\<磁碟機 > \ 或 Program Files (x86) \Microsoft SQL Server 2012 DMAdd-Ins):  
  
-   **Microsoft Data Mining.vst**此範本包含預先設計的格式設定、 配置及精靈，可協助您使用資料採礦圖形。  
  
-   **Microsoft Data Mining Shape Studio.vss**這個樣板檔案包含與範本相關聯的圖形。  
  
## <a name="how-to-use-the-templates"></a>如何使用範本  
 若要開啟範本，您可以按兩下圖形檔，也可以開啟 Visio 然後再開啟圖形範本。  
  
1.  從樣板將其中一個 Visio 資料採礦圖形置於新頁面上。  
  
2.  精靈啟動時，請連接到存有您想要顯示之資料採礦模型的伺服器。  
  
3.  選取資料採礦模型，讓模型類型符合視覺化類型。  
  
4.  設定應該要如何顯示及格式化資料的選項。  
  
5.  完成後**資料採礦圖形精靈**，您有圖表，您可以修改並增強使用 Visio 的功能。  
  
 如需如何處理及增強 Visio 模型圖表的詳細資訊，請參閱[檢視資料採礦模型在 Visio 中&#40;資料採礦增益集&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)  
  
## <a name="requirements"></a>需求  
  
-   若要使用範本，您必須先建立與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。  
  
     精靈會提示您選取 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器及指定包含採礦模型的資料庫。  
  
     如需有關如何建立連接的資訊，請參閱 <<c0> [ 連接至來源的資料&#40;適用於 Excel 的資料採礦用戶端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。</c0>  
  
-   如果您使用資料表分析工具，請務必將模型儲存至 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器，切勿使用暫時性模型。  
  
-   模型必須已使用其中一種支援的演算法建立：群集、決策樹、類神經網路、貝氏機率分類或羅吉斯迴歸。  
  
  
