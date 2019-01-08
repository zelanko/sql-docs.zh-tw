---
title: Analysis Services 表格式模型資料表屬性 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e5104eacafe60ab3fd1ea1ff29cc64b8453e4ff7
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072005"
---
# <a name="table-properties"></a>資料表屬性 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  這篇文章描述表格式模型資料表屬性。 這裡所述的屬性與 [編輯資料表屬性] 對話方塊中的屬性不同，後者會定義從來源匯入的資料行。  
  
 本主題的章節：  
  
-   [資料表屬性](#bkmk_properties)  
  
-   [設定資料表屬性設定](#bkmk_config_prop)  
  
##  <a name="bkmk_properties"></a> 資料表屬性  
 **基本**  
  
|屬性|預設值|描述|  
|--------------|---------------------|-----------------|  
|**連接名稱**|\<連線名稱 >|資料表的資料來源的連接名稱。<br /><br /> 若要編輯連接，請按一下此按鈕。|  
|**Hidden**|False|指定是否在報表用戶端欄位清單中隱藏資料表。|  
|**資料分割**||資料表的資料分割無法在 **[屬性]** 視窗中顯示。 若要檢視、建立或編輯資料分割，請按一下此按鈕以開啟 [資料分割管理員]。|  
|**來源資料**||資料表的來源資料無法在 **[屬性]** 視窗中顯示。 若要檢視或編輯來源資料，請按一下此按鈕以開啟 [編輯資料表屬性] 對話方塊。|  
|**資料表描述**||資料表的文字描述。<br /><br /> 在 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]中，如果使用者將游標置於欄位清單內這個資料表的上方，將以工具提示的形式顯示說明。|  
|**資料表名稱**|\<好記名稱 >|指定資料表的易記名稱。 資料表名稱可在使用 [資料表匯入精靈] 匯入資料表時指定，或在匯入後隨時指定。 模型中的資料表名稱可以不同於在來源的關聯資料表。 資料表易記名稱出現在報表用戶端應用程式欄位清單中以及 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的模型資料庫。|  
  
 **報表屬性**  
  
 詳細的描述和報告屬性的組態資訊，請參閱[Power View 報表屬性](../../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md)。  
  
|屬性|預設值|描述|  
|--------------|---------------------|-----------------|  
|**預設欄位集**|||  
|資料表行為|||  
  
##  <a name="bkmk_config_prop"></a> 設定資料表屬性設定  
  
1.  在模型設計師的 [資料檢視] 中按一下資料表 (索引標籤)，或在 [圖表檢視] 中按一下資料表標頭。  
  
2.  在 **[屬性]** 視窗中按一下屬性，然後輸入值，或按一下按鈕來選取其他組態選項。  
  
  
