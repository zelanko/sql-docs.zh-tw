---
title: 物件命名規則 (Analysis Services) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b10662d32952565ccf7b30a6615470d2557749f3
ms.sourcegitcommit: 2a47e66cd6a05789827266f1efa5fea7ab2a84e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/31/2018
ms.locfileid: "43348639"
---
# <a name="object-naming-rules-analysis-services"></a>物件命名規則 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  本主題將描述物件命名慣例以及任何物件名稱 (以 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的程式碼或指令碼形式) 中無法使用的保留字和字元。  
  
##  <a name="bkmk_Names"></a> 命名慣例  
 每個物件都**名稱**並**識別碼**父集合的範圍內必須是唯一的屬性。 例如，兩個維度可以擁有相同的名稱，前提是每個維度都位在不同的資料庫內。  
  
 雖然您可以手動指定**識別碼**是通常是自動產生建立物件時。 您應該永遠不會變更**識別碼**當您開始建立模型。 在整個模型的所有物件參考都根據**識別碼**。 因此，變更**識別碼**很容易導致模型損毀。  
  
 **資料來源**並**DataSourceView**物件都有命名慣例值得注意的例外狀況。 **資料來源**識別碼可以設定為單一點 （.），這不是唯一的做為參考，目前的資料庫。 第二個例外狀況**DataSourceView**，它會遵守針對定義的命名慣例**資料集**物件，在.NET Framework 中，其中**名稱**做為識別項。  
  
 下列規則適用於**名稱**並**識別碼**屬性。  
  
-   名稱不區分大小寫。 您在相同資料庫中不能同時有一個名為 "sales" 的 Cube 和另一個名為 "Sales" 的 Cube。  
  
-   物件名稱中不允許有任何開頭或尾端空白，但是您可以在名稱中內嵌空白。 開頭和尾端空白會以隱含方式加以修剪。 這同時適用於**名稱**並**識別碼**的物件。  
  
-   最大字元數為 100。  
  
-   識別項的第一個字元沒有特殊規定。 第一個字元可能會是任何有效的字元。  
  
##  <a name="bkmk_reserved"></a> 保留的字和字元  
 保留字為英文，而且會套用到物件名稱，而不是標題。 如果您不小心在物件名稱中使用保留字，將會發生驗證錯誤。 如果是多維度和資料採礦模型，底下所述的保留字在任何時候都無法在任何物件名稱中使用。  
  
 如果是資料庫相容性設定為 1103 的表格式模型，對於不符合擴充字元要求及某些用戶端應用程式命名慣例的特定物件而言，驗證規則已經鬆綁。 符合這些準則的資料庫受限於比較不嚴謹的驗證規則。 在此情況下，有可能物件名稱包含受限的字元而且依然通過驗證。  
  
 **保留文字**  
  
-   AUX  
  
-   CLOCK$  
  
-   COM1 到 COM9 (COM1、COM2、COM3 等等)  
  
-   CON  
  
-   LPT1 到 LPT9 (LPT1、LPT2、LPT3 等等)  
  
-   NUL  
  
-   PRN  
  
-   在 XML 中，不允許使用 NULL 當做任何字串中的字元  
  
 **保留的字元**  
  
 下表列出特定物件的無效字元。  
  
|Object|無效字元|  
|------------|------------------------|  
|**Server**|在命名伺服器物件時要遵守 Windows 伺服器命名慣例。 請參閱[命名慣例 (Windows)](/windows/desktop/DNS/naming-conventions)如需詳細資訊。|  
|**DataSource**|: / \ * &#124; ? "（) [] {} <>|  
|**層級**或**屬性**|. , ; ' ` : / \ * &#124; ? " & % $ ! + = [] {} < >|  
|**維度**或**階層**|. , ; ' ` : / \ * &#124; ? " & % $ ! + = （) [] {} \<，>|  
|所有其他物件|. , ; ' ` : / \ * &#124; ? " & % $ ! + = （) [] {} < >|  
  
 **例外狀況： 當允許保留的字元是**  
  
 如前所述，具有特定模式和相容性層級的資料庫可以擁有包含保留字元的物件名稱。 如果是允許使用擴充字元的表格式資料庫 (1103 或更高層級)，維度屬性、階層、層級、量值和 KPI 物件名稱可以包含保留字元：  
  
|伺服器模式和資料庫相容性層級|允許保留的字元嗎？|  
|--------------------------------------------------|----------------------------------|  
|MOLAP (所有版本)|否|  
|表格式 - 1050|否|  
|表格式 - 1100|否|  
|表格式 – 1130 和更高版本|是|  
  
 資料庫可以有 ModelType 預設值。 預設值相當於多維度，因此不支援在資料行名稱中使用保留的字元。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 保留字](../../../mdx/mdx-reserved-words.md)   
 [Analysis Services 中的翻譯支援](../../../analysis-services/translation-support-in-analysis-services.md)   
 [XML for Analysis 符合&#40;XMLA&#41;](../../../analysis-services/xmla/xml-for-analysis-compliance-xmla.md)  
  
  
