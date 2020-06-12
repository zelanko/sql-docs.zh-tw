---
title: 連接到一般檔案（SSAS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connflatfile.f1
ms.assetid: a365991e-eded-4cd8-89c0-0daf6d658d15
author: minewiskan
ms.author: owend
ms.openlocfilehash: 970a55b709e164da573fbd224c13cc641a3ba06a
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527194"
---
# <a name="connect-to-a-flat-file-ssas"></a>連接到一般檔案 (SSAS)
  [資料表匯入精靈]**** 的這個頁面可讓您連接到一般檔案 (.txt)、Tab 分隔的檔案 (.tab) 或逗號分隔的檔案 (.csv)。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。  
  
 若要連接至一般檔案，您必須先在電腦上安裝適當的 ACE 提供者。 如需詳細資訊，請參閱[支援的資料來源 &#40;SSAS 表格式&#41;](tabular-models/data-sources-supported-ssas-tabular.md)。  
  
> [!NOTE]  
>  在這個頁面中選取檔案時，會使用目前使用者的認證。 不過，如果在 [模擬資訊] 頁面中指定的使用者未具備從所選檔案讀取的權限，則匯入將不會成功。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 **易記連接名稱**  
 為此資料來源連接輸入唯一的名稱。 這是必要的欄位。  
  
 **檔案路徑**  
 指定檔案的完整路徑。  
  
 **瀏覽**  
 導覽至可以使用檔案的位置。  
  
 **資料行分隔符號**  
 從可用資料行分隔符號的清單中選取。 請選擇不太可能會在文字中出現的分隔符號。  
  
|值|Description|  
|-----------|-----------------|  
|定位字元 (t)|資料行是以定位字元 (t) 分隔。|  
|逗號 (,)|資料行是以逗號 (,) 分隔。|  
|分號 (;)|資料行是以分號 (;) 分隔。|  
|空格 ( )|資料行是以空格 ( ) 分隔。|  
|冒號 (:)|資料行是以冒號 (:) 分隔。|  
|分隔號 (&#124;)|資料行是以分隔號 (&#124;) 分隔。|  
  
 **進階**  
 指定一般檔案的編碼方式和地區設定選項。  
  
 **使用第一個資料列做為資料行標頭**  
 指定是否要使用第一個資料列做為目的地資料表的資料行標頭。  
  
 **資料預覽**  
 預覽所選檔案中的資料，然後使用下列選項修改資料匯入。  
  
> [!NOTE]  
>  只有檔案中的前 50 個資料列會顯示在這個預覽中。  
  
|選項|描述|  
|------------|-----------------|  
|**資料行標頭中的核取方塊**|選取核取方塊可將資料行納入資料匯入作業。 清除核取方塊可從資料匯入作業排除資料行。|  
|**資料行標頭中的向下箭號按鈕**|排序及篩選資料行中的資料。|  
  
 **清除資料列篩選**  
 移除已經套用到資料行中資料的所有篩選。  
  
  
