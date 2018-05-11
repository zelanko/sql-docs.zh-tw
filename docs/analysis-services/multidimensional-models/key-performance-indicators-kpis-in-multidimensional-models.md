---
title: 關鍵效能指標 (Kpi) 多維度模型中的 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 97267b17ed792668bfc7fde5d0e38621867a5ee2
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="key-performance-indicators-kpis-in-multidimensional-models"></a>多維度模型中的關鍵效能指標 (KPI)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在商務用語中，關鍵效能指標 (KPI) 是量測商務成就的可量化度量。  
  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，關鍵效能指標是用來評估商務成就的計算集合，這些計算與 Cube 中的量值群組相關。 一般來說，這些計算是多維度運算式 (MDX) 運算式或導出成員的結合。 KPI 也有其他中繼資料，這些中繼資料會提供有關用戶端應用程式應該如何顯示 KPI 計算結果的資訊。  
  
 KPI 會處理有關目標集合、Cube 中記錄之效能的實際公式，以及顯示趨勢與效能狀態度量的相關資訊。 AMO 會用來定義公式及有關 KPI 值的其他定義。 查詢介面 (如 ADOMD.NET) 是由用戶端應用程式用來擷取 KPI 值，並對使用者公開 KPI 值。 如需詳細資訊，請參閱 [使用 ADOMD.NET 來開發](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)。  
  
 簡單的 <xref:Microsoft.AnalysisServices.Kpi> 物件是由基本資訊、目標、達到的實際值、狀態值、趨勢值，以及檢視 KPI 的資料夾所組成。 基本資訊包括 KPI 的名稱和描述。 目標是評估為某個數字的 MDX 運算式。 實際值是評估為某個數字的 MDX 運算式。 狀態和趨勢值是評估為某個數字的 MDX 運算式。 資料夾是要呈現給用戶端之 KPI 的建議位置。  
  
 在商務用語中，關鍵效能指標 (KPI) 是量測商務成就的可量化度量。 KPI 通常會在一段時間內進行評估。 例如，組織的業務部門可能使用每月毛利作為關鍵效能指標，但同一個組織的人力資源部門則可能使用每季員工的流動率。 每一個都是 KPI 的範例。 高階管理人員經常會耗用在商務計分卡中分組的 KPI，以取得商務成就之快速與精確的記錄摘要。  
  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，關鍵效能指標是用來評估商務成就的計算集合，這些計算與 Cube 中的量值群組相關。 一般來說，這些計算是多維度運算式 (MDX) 運算式和導出成員的結合。 KPI 也有其他中繼資料，這些中繼資料會提供有關用戶端應用程式應該如何顯示 KPI 計算結果的資訊。  
  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，KPI 的一個主要優點是它們均為可由不同用戶端應用程式耗用的伺服器架構 KPI。 與不同用戶端應用程式的不同版本真實性相比，伺服器型 KPI 呈現單一版本的真實性。 甚至，在伺服器上而非每部用戶端電腦上執行有時複雜的計算，也可能會對效能提升有所助益。  
  
## <a name="common-kpi-terms"></a>常見 KPI 詞彙  
 下表提供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中常見 KPI 詞彙的定義。  
  
|詞彙|定義|  
|----------|----------------|  
|目標|會傳回 KPI 目標值的 MDX 數值運算式或計算。|  
|Value|會傳回實際 KPI 值的 MDX 數值運算式。|  
|狀態|代表特定時間點之 KPI 狀態的 MDX 運算式。<br /><br /> 狀態 MDX 運算式應傳回介於 -1 和 1 之間的正規化值。 等於或小於 -1 的值將解譯為「不良」或「低」。 零值 (0) 會解釋為「可接受」或「中」。 等於或大於 1 的值將解譯為「很好」或「高」。<br /><br /> 可以選擇性地傳回無限數量的中繼值，而且如果用戶端應用程式支援的話，也可用來顯示任意數量的其他狀態。|  
|趨勢|評估一段時間後之 KPI 值的 MDX 運算式。 趨勢可以是在特定商務內容中任何有意義且以時間為基礎的準則。<br /><br /> 趨勢 MDX 運算式可讓商務使用者判斷經過一段時間之後，KPI 是提升還是降低。|  
|狀態指標|快速表示 KPI 狀態的視覺元素。 元素的顯示取決於用來評估狀態的 MDX 運算式值。|  
|趨勢指標|快速表示 KPI 趨勢的視覺元素。 元素的顯示取決於用來評估趨勢的 MDX 運算式值。|  
|顯示資料夾|使用者瀏覽 Cube 時，可在其中看到 KPI 的資料夾。|  
|父 KPI|現有 KPI 的參考，其中使用子 KPI 的值來計算父 KPI。 有時單一 KPI 會是由其他 KPI 值構成的計算。 此屬性有助於在用戶端應用程式中，使父 KPI 之下的子 KPI 可以正確顯示。|  
|目前時間成員|會傳回成員的 MDX 運算式，該成員會用來識別 KPI 的暫時內容。|  
|Weight|指定 KPI 之相對重要性的 MDX 數值運算式。 如果 KPI 已指派給父 KPI，則在計算父 KPI 值時，可使用加權來按比例調整子 KPI 值的結果。|  
  
## <a name="parent-kpis"></a>父 KPI  
 組織可追蹤不同層級的不同商業標準。 例如，只有兩或三個 KPI 可用來量測全公司的商業成就，但這些公司的整體性 KPI 可以用公司內的事業單位所追蹤的其他三或四個 KPI 為基礎。 同時，公司內的事業單位可使用不同的統計資料來計算相同的 KPI，然後再將結果積存到公司的整體性 KPI。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]可讓您定義 Kpi 之間的父子式關聯性。 此父子式關聯性可讓子 KPI 的結果用於計算父 KPI 的結果。 用戶端應用程式也可以使用此關聯性來適當地顯示父 KPI 和子 KPI。  
  
## <a name="weights"></a>加權  
 子 KPI 也可指派加權。 加權可讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在計算父 KPI 值時，按比例調整子 KPI 的結果。  
  
## <a name="retrieving-and-displaying-kpis"></a>擷取及顯示 KPI  
 關鍵效能指標的顯示取決於用戶端應用程式的實作。 例如，在 Cube 設計師 [KPI] 索引標籤的工具列上選取 [瀏覽器檢視]，就會示範一個可能的用戶端實作，其中利用圖形來顯示狀態和趨勢指標、顯示用來群組 KPI 的資料夾，以及顯示在父 KPI 之下的子 KPI。  
  
 您可以使用 MDX 函數來擷取 MDX 的個別區段，例如值或目標，以使用於 MDX 運算式、陳述式和指令碼。  
  
  
