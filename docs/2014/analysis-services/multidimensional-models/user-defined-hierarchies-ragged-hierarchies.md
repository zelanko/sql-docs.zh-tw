---
title: 不完全階層 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ragged hierarchies [Analysis Services]
ms.assetid: e40a5788-7ede-4b0f-93ab-46ca33d0cace
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 533abbb47db40f16c0d7d5e4d85851975c89e23d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889326"
---
# <a name="ragged-hierarchies"></a>不完全階層
  不完全階層是所含層級數目不平均的使用者定義階層。 常見範例包括組織圖 (高階主管同時擁有部門主管級和非主管級直屬員工)，或由國家/地區-區域-城市組成的地理階層 (其中部分城市缺少父州或省，例如華盛頓特區、梵蒂岡或新德里)。  
  
 維度中大多數階層每一個層級的上一層級，其成員數與相同層級的任何其他成員相同。 不完全階層的不同之處在於，至少一個成員的邏輯父成員不在成員的上一層級內。 若發生此情形，階層會向下延伸至不同層級的不同鑽研路徑。 在用戶端應用程式中，這會使得向下鑽研路徑變得很複雜。  
  
 用戶端應用程式在處理不完全階層的程度方面各有不同。 如果您的模型中存在不完全階層，則需要執行一些額外的工作，才能取得預期的轉譯行為。  
  
 第一個步驟是查看用戶端應用程式如何處理向下鑽研路徑。 例如，Excel 會將父項名稱當做遺漏值的預留位置來重複。 若要自行查看這個行為，請在 Adventure Works 多維度模型中使用 Sales Territory 維度建置樞紐分析表。 在具有「銷售地區」屬性「群組」、「國家/地區」和「區域」的樞紐分析表中，您會看到遺漏區域值的國家/地區會取得預留位置，在本例中，會重複其父項 (國家/地區名稱)。 此行為衍生自 Excel 固有的連接字串屬性 MDX Compatibility=1。 如果用戶端未正常提供您所需的向下鑽研行為，您可以設定模型中的屬性，至少變更其中一些行為。  
  
 本主題包含下列幾節：  
  
-   [修改不完全階層中之向下鑽研導覽的方法](#bkmk_approach)  
  
-   [設定 HideMemberIf 以隱藏一般階層中的成員](#bkmk_Hide)  
  
-   [設定 MDX 相容性以決定如何在用戶端應用程式中表示預留位置](#bkmk_Mdx)  
  
##  <a name="bkmk_approach"></a> 修改不完全階層中之向下鑽研導覽的方法  
 向下鑽研導覽未傳回預期的值或視為使用不便時，不完全階層的存在將成為問題。 若要修正不完全階層所導致的問題，請考量以下選項：  
  
-   使用一般階層，但是在每個層級上設定 `HideMemberIf` 屬性來指定使用者是否可看到遺漏的層級。 設定 `HideMemberIf` 時，您也應該在連接字串中設定 `MDXCompatibility` 以覆寫預設導覽行為。 本主題將提供設定這些屬性的指示。  
  
-   建立可以明確方式管理層級成員的父子式階層。 如需此技術的說明，請參閱 [Ragged Hierarchy in SSAS (blog post)](http://dwbi1.wordpress.com/2011/03/30/ragged-hierarchy-in-ssas/)(SSAS 中的不完全階層 (部落格文章))。 如需《線上叢書》中的詳細資訊, 請參閱[父子式](parent-child-dimension.md)階層。 建立父子式階層的缺點在於，每個維度只能有一個父子式階層，且當您計算中繼成員的彙總時，通常會導致效能降低。  
  
 如果您的維度包含多個不完全階層，您應該使用第一種方法：設定 `HideMemberIf`。 在使用不完全階層方面有實務經驗的 BI 開發人員，可進一步支援實體資料表中的其他變更，並建立每個層級的個別的資料表。 如需這項技術的詳細資訊, 請參閱[聖馬丁 Mason 的 SSAS 財務 Cube-第1A 層-不完全階層 (blog)](http://martinmason.wordpress.com/2012/03/03/the-ssas-financial-cubepart-1aragged-hierarchies-cont/) 。  
  
##  <a name="bkmk_Hide"></a> 設定 HideMemberIf 以隱藏一般階層中的成員  
 在不完全維度的資料表中，在邏輯上遺漏的成員可以不同方式來表示。 資料表資料格可包含 Null 或空字串，或者它們可以包含與它們父系相同的值以做為一個預留位置。 預留位置的表示是由子成員的預留位置狀態 (如同 `HideMemberIf` 屬性所決定) 以及用戶端應用程式的 `MDX Compatibility` 連接字串屬性所決定。  
  
 如果是支援不完全階層顯示的用戶端應用程式，您可以使用這些屬性來隱藏在邏輯上遺漏的成員。  
  
1.  在 SSDT 中按兩下維度，在維度設計師中加以開啟。 第一個索引標籤 [維度結構] 會在 [階層] 窗格中顯示屬性階層。  
  
2.  以滑鼠右鍵按一下此階層中的成員，並選取 [屬性]。 將 `HideMemberIf` 設定為底下描述的其中一個值。  
  
    |HideMemberIf 設定|描述|  
    |--------------------------|-----------------|  
    |`Never`|永不隱藏層級成員。 這是預設值。|  
    |**OnlyChildWithNoName**|當層級成員是父系的唯一子系，且其名稱是 Null 或空白字串時，會隱藏層級成員。|  
    |**OnlyChildWithParentName**|當層級成員是父系的唯一子系，且其名稱與其父系名稱相同時，會隱藏層級成員。|  
    |**NoName**|當層級成員名稱空白時，會隱藏層級成員。|  
    |**ParentName**|當層級成員名稱與其父系名稱相同時，會隱藏層級成員。|  
  
##  <a name="bkmk_Mdx"></a> 設定 MDX 相容性以決定如何在用戶端應用程式中表示預留位置  
 在階層層級上設定 `HideMemberIf` 之後，您也應該在從用戶端應用程式傳送的連接字串中設定 `MDX Compatibility` 屬性。 `MDX Compatibility` 設定會決定是否使用 `HideMemberIf`。  
  
|MDX 相容性設定|描述|使用量|  
|-------------------------------|-----------------|-----------|  
|**1**|顯示預留位置的值。|這是 Excel、SSDT 和 SSMS 使用的預設值。 它會指示伺服器在不完全階層中向下鑽研空的層級時，傳回預留位置的值。 如果您按一下預留位置的值，您可以繼續往下前往子節點 (分葉節點)。<br /><br /> Excel 擁有用來連接到 Analysis Services 的連接字串，而且它永遠都會針對每個新的連接將 `MDX Compatibility` 設定為 1。 這個行為會保留回溯相容性。|  
|**2**|隱藏預留位置的值 (Null 值或父層級的重複)，但是會顯示具有相關值的其他層級和節點。|就不完全階層而言，`MDX Compatibility`=2 通常會視為慣用設定。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表和某些協力廠商用戶端應用程式可以保留這項設定。|  
  
## <a name="see-also"></a>另請參閱  
 [建立使用者定義階層](user-defined-hierarchies-create.md)   
 [使用者階層](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [父子式階層](parent-child-dimension.md)   
 [連接字串屬性 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/instances/connection-string-properties-analysis-services)  
  
  
