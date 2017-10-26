---
title: "資料行屬性 (SSAS 表格式) |Microsoft 文件"
ms.custom: 
ms.date: 05/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.columnprop.f1
ms.assetid: 4046c1a3-46c7-47db-b355-52e9c2f23671
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 09e1b0f4a10c179dc9b4fe3055710063fc46a2bb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="column-properties-ssas-tabular"></a>資料行屬性 (SSAS 表格式)
  本主題描述表格式模型資料行屬性。  
  
>  [!NOTE]  
>  所有的相容性層級不支援某些屬性。    
  
##  <a name="bkmk_properties"></a> 資料行屬性  
**進階**  
  
|屬性|預設值|Description|  
|--------------|---------------------|-----------------|  
|**顯示資料夾**||組織中用戶端應用程式欄位清單的資料行的單一或巢狀資料夾。|  

**Basic**  
  
|屬性|預設值|說明|  
|--------------|---------------------|-----------------|  
|**資料行名稱**||儲存在模型內以及顯示於報告用戶端欄位清單中的資料行名稱。|  
|**資料格式**|匯入期間自動決定。|指定要用於此資料行中之資料的顯示格式。 此屬性具有以下選項：<br /><br /> **一般**<br /><br /> **十進位數字**<br /><br /> **整數**<br /><br /> **貨幣**<br /><br /> **百分比**<br /><br /> **科學記號**<br /><br /> 當您設定資料格式後，可以設定每一個格式特有的屬性。 例如，如果您選擇 **[貨幣]** 格式，則可以設定可見小數位數，然後依次選擇千位分隔符號和貨幣符號。<br /><br /> <br /><br /> 如果資料行的值包含影像，請參考 **[代表影像]**。|  
|**資料類型**|匯入期間自動決定。|針對資料行中的所有值指定資料類型。|  
|**說明**||資料行的文字描述。<br /><br /> 在某些報告用戶端中，如果使用者將游標置於欄位清單內這個資料行的上方，將以工具提示的形式顯示說明。|  
|**Hidden**|False|指定是否在報告用戶端欄位清單中隱藏資料行。<br /><br /> 將此屬性設為 **[True]** 可在顯示中隱藏這個資料行。 例如，包含識別碼或索引鍵的資料行通常對使用者沒有用處。<br /><br /> 如果您在報告用戶端中隱藏資料行，則模型資料中不會隱藏此欄位。 如果您針對模型建立查詢，還是可以看到此欄位。 隱藏的資料行依然可以用於分組或排序。<br /><br /> **[隱藏]** 屬性不提供任何形式的資料安全性。 若要保護資料安全，請在角色中使用資料列篩選。 如需詳細資訊，請參閱 [角色 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)。|  
|**依資料行排序**||指定另一個資料行來排序這個資料行中的值。 兩個資料行之間必須有關聯性存在。<br /><br /> 這個值必須是現有資料行的名稱。 您不能指定公式或量值。|  

 **其他**  
  
|屬性|預設值|Description|  
|--------------|---------------------|-----------------|  
|**編碼的提示**|預設值|指定編碼方式來最佳化處理。 編碼值，可以改善查詢效能，通常用於彙總的數值資料行。 雜湊編碼為群組依據資料行 （通常是維度資料表值） 和外部索引鍵。 字串資料行一律會編碼的雜湊。|  

 **報表屬性**  
  
|屬性|預設值|說明|  
|--------------|---------------------|-----------------|  
|預設影像|False|指定哪個資料行提供代表資料列資料的影像 (例如員工記錄的相片識別碼)。|  
|預設標籤|False|指定哪個資料行提供代表資料列資料的顯示名稱 (例如員工記錄的員工姓名)。|  
|影像 URL/資料目錄 (SP1)|False|指定這個資料行中的值做為伺服器上影像的超連結。 例如： `http://localhost/images/image1.jpg`。|  
|保留唯一資料列|False|指定哪些資料行提供應視為唯一的值，即使是重複值也一樣 (例如，員工姓氏和名字，以因應兩個以上同名員工的案例)。|  
|資料列識別碼|False|指定只包含唯一值的資料行，允許該資料行做為內部群組索引鍵使用。|  
|摘要方式|預設值|將這個資料行加入至欄位清單時，指定報表用戶端工具會為資料行計算套用彙總函式 Sum。 若要變更預設計算，請從下拉式清單中選取適當函式。 這個屬性只適用於可彙總類型的資料行。|  
|資料表詳細資料位置|無預設欄位集|指定這個資料行或量值可加入至單一資料表的一組欄位，以增強報表用戶端中的資料表視覺效果經驗。|  
  
##  <a name="bkmk_config_prop"></a> 設定資料行屬性設定  
  
1.  在模型設計師中，選取資料表中的資料行。  
  
2.  在 **[屬性]** 視窗中按一下屬性，然後輸入值，或按一下向下箭頭來選取設定選項。  
  
## <a name="see-also"></a>另請參閱  
 [Power View 報表屬性](../../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md)   
 [隱藏或凍結資料行](../../analysis-services/tabular-models/hide-or-freeze-columns-ssas-tabular.md)   
 [在資料表新增資料行](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)  
  
  

