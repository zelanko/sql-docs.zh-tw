---
title: 物件命名規則 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], naming
ms.assetid: b338a60d-4802-4b68-862a-6dc6a3f75e48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dce01d84be7f2850f916b21ccb02fb7cd24a6cdc
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158884"
---
# <a name="object-naming-rules-analysis-services"></a>物件命名規則 (Analysis Services)
  本主題將描述物件命名慣例以及任何物件名稱 (以 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的程式碼或指令碼形式) 中無法使用的保留字和字元。  
  
##  <a name="bkmk_Names"></a> 命名慣例  
 每個物件都有在父集合的範圍內必須是唯一的 `Name` 和 `ID` 屬性。 例如，兩個維度可以擁有相同的名稱，前提是每個維度都位在不同的資料庫內。  
  
 雖然您可以手動指定它，但是在建立物件時通常會自動產生 `ID`。 一旦您開始建立模型之後，絕對不要變更 `ID`。 整個模型中的所有物件參考都是根據 `ID`。 因此，變更 `ID` 很容易導致模型損毀。  
  
 `DataSource` 和 `DataSourceView` 物件有顯著的命名慣例例外。 `DataSource` 識別碼可以設定為一個非唯一的點 (.)，當做目前資料庫的參考。 第二個例外狀況為 `DataSourceView`，它會遵守針對 .NET Framework 中的 `DataSet` 物件所定義的命名慣例，其中會使用 `Name` 當做識別碼。  
  
 下列規則會套用到 `Name` 和 `ID` 屬性。  
  
-   名稱不區分大小寫。 您不能有一個名為"sales"的 cube 和另一個相同的資料庫中名為"Sales"。  
  
-   物件名稱中不允許有任何開頭或尾端空白，但是您可以在名稱中內嵌空白。 開頭和尾端空白會以隱含方式加以修剪。 這同樣適用於物件的 `Name` 和 `ID`。  
  
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
|`Server`|在命名伺服器物件時要遵守 Windows 伺服器命名慣例。 請參閱[命名慣例 (Windows)](/windows/desktop/DNS/naming-conventions)如需詳細資訊。|  
|`DataSource`|`: / \ * | ? " () [] {} <>`|  
|`Level` 或 `Attribute`|```. , ; ' ` : / \ * &| ? " & % $ ! + = [] {} \< >```|  
|`Dimension` 或 `Hierarchy`|```. , ; ' ` : / \ * | ? " & % $ ! + = () [] {} \<,>```|  
|所有其他物件|```. , ; ' ` : / \ * | ? " & % $ ! + = () [] {} \< >```|  
  
 **例外狀況：當允許保留的字元**  
  
 如前所述，具有特定模式和相容性層級的資料庫可以擁有包含保留字元的物件名稱。 如果是允許使用擴充字元的表格式資料庫 (1103 或更高層級)，維度屬性、階層、層級、量值和 KPI 物件名稱可以包含保留字元：  
  
|伺服器模式和資料庫相容性層級|允許保留的字元嗎？|  
|--------------------------------------------------|----------------------------------|  
|MOLAP (所有版本)|否|  
|表格式 - 1050|否|  
|表格式 - 1100|否|  
|表格式-1130年和更高版本|是|  
  
 資料庫可以有 ModelType 預設值。 預設值相當於多維度，因此不支援在資料行名稱中使用保留的字元。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 保留字](/sql/mdx/mdx-reserved-words)   
 [翻譯&#40;Analysis Services&#41;](../../../analysis-services/translations-analysis-services.md)   
 [XML for Analysis 符合&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-compliance-xmla)  
  
  
