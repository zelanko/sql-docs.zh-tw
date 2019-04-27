---
title: 角色 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: e547382a-c064-4bc6-818c-5127890af334
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d1b59b0e279d016d2fcaee9b0fcae6742c4ff87b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62756901"
---
# <a name="roles-ssas-tabular"></a>角色 (SSAS 表格式)
  表格式模型中的角色定義模型的成員權限。 每個角色都包含成員 (依 Windows 使用者名稱或 Windows 群組列出) 和權限 (讀取、處理、系統管理員)。 角色的成員可以依角色權限所定義，對模型執行動作。 以讀取權限定義的角色也可以使用資料列層級篩選，在資料列層級提供額外的安全性。  
  
> [!IMPORTANT]  
>  為了讓使用者可以使用報表或資料分析用戶端應用程式連接至已部署的模型，您必須至少建立一個具有「讀取」權限的角色，並讓這些使用者成為該角色的成員。  
  
 本主題中的資訊適用於使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的 [角色管理員] 對話方塊來定義角色的表格式模型作者。 在模型製作期間定義的角色會套用至模型工作空間資料庫。 部署模型資料庫之後，模型資料庫管理員即可使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，來管理 (加入、編輯、刪除) 角色成員。 若要了解如何在已部署的資料庫中管理角色成員，請參閱[表格式模型角色 &#40;SSAS 表格式&#41;](tabular-model-roles-ssas-tabular.md)。  
  
 [表格式模型化 &#40;Adventure Works 教學課程&#41;](../tabular-modeling-adventure-works-tutorial.md) 包含如何使用此功能的其他資訊和課程。  
  
 本主題的章節：  
  
-   [了解角色](#bkmk_underst)  
  
-   [Permissions](#bkmk_permissions)  
  
-   [資料列篩選](#bkmk_rowfliters)  
  
-   [測試角色](#bkmk_testroles)  
  
-   [相關工作](#bkmk_rt)  
  
##  <a name="bkmk_underst"></a> 了解角色  
 您可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，使用角色來管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和資料的安全性。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]有兩種角色類型：  
  
-   伺服器角色，這是一種固定角色，提供對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體的管理員存取權。  
  
-   資料庫角色，這是模型作者和管理員所定義的角色，用來控制非管理員使用者對模型資料庫和資料的存取。  
  
 針對表格式模型定義的角色就是資料庫角色。 換句話說，這些角色的成員是由 Windows 使用者或群組所組成，具有定義成員可對模型資料庫執行之動作的特定權限。 資料庫角色會建立成資料庫中的個別物件，且只適用於建立該角色的資料庫。 預設具有工作空間資料庫伺服器之「系統管理員」權限的模型作者，可以將 Windows 使用者及/或 Windows 群組加入至角色；或者針對已部署的模型，由管理員加入。  
  
 表格式模型中的角色可以進一步透過資料列篩選定義。 資料列篩選使用 DAX 運算式定義使用者可以查詢的資料表資料列，以及許多方向的任何相關資料列。 只有「讀取」及「讀取和處理」權限，才可以定義使用 DAX 運算式的資料列篩選。 如需詳細資訊，請參閱本主題稍後的 [資料列篩選](#bkmk_rowfliters) 。  
  
 根據預設，當您建立新的表格式模型專案時，模型專案沒有任何角色。 您可以使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中的 [角色管理員] 對話方塊來定義角色。 在模型撰寫期間定義角色時，會將這些角色套用至模型工作空間資料庫。 部署模型時，會將相同的角色套用至已部署的模型。 部署模型之後，伺服器角色的成員 ([!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理員) 和資料庫管理員即可使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，來管理與模型相關聯的角色及與每個角色相關聯的成員。  
  
> [!NOTE]  
>  針對在 DirectQuery 模式下設定之模型所定義的角色無法使用資料列篩選，但是會套用為每個角色定義的權限。  
  
##  <a name="bkmk_permissions"></a> 權限  
 每一個角色都有一個已定義的資料庫權限 (但不包括「讀取和處理」結合權限)。 新角色的預設權限為「無」。 換句話說，成員一旦加入至具有「無」權限的角色後，除非授與其他權限，否則將無法修改資料庫、執行處理作業、查詢資料或查看資料庫。  
  
 Windows 群組或使用者可以是任何數目角色的成員，且每個角色具有不同的權限。 當使用者是多個角色的成員時，針對每個角色定義的權限會累計。 例如，如果某位使用者是具有「讀取」權限之角色的成員，同時也是具有「無」權限之角色的成員，則該使用者將具有「讀取」權限。  
  
 每個角色可以定義下列其中一個權限：  
  
|Permissions|描述|使用 DAX 的資料列篩選|  
|-----------------|-----------------|----------------------------|  
|None|成員無法對模型資料庫結構描述進行任何修改，也無法查詢資料。|不會套用資料列篩選。 此角色的使用者看不到任何資料|  
|讀取|允許成員查詢資料 (根據資料列篩選)，但是無法在 SSMS 中看到模型資料庫，也無法對模型資料庫結構描述做任何變更，使用者也無法處理模型。|可套用資料列篩選。 使用者只能看到資料列篩選 DAX 公式中指定的資料。|  
|讀取和處理|成員可以查詢資料 (根據資料列層級篩選)，並透過執行指令碼或包含處理命令的封裝來執行處理作業，但無法對資料庫進行任何變更。 無法在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中檢視模型資料庫。|可套用資料列篩選。 只能查詢資料列篩選 DAX 公式中指定的資料。|  
|處理|成員可以透過執行指令碼或包含處理命令的封裝來執行處理作業。 無法修改模型資料庫結構描述。 無法查詢資料。 無法在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中查詢模型資料庫。|不會套用資料列篩選。 無法查詢此角色中的任何資料|  
|系統管理員|成員可以對模型結構描述進行修改，也可以在模型設計師、報表用戶端及 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中查詢所有資料。|不會套用資料列篩選。 可以查詢此角色中的所有資料。|  
  
##  <a name="bkmk_rowfliters"></a> 資料列篩選  
 資料列篩選會定義特定角色的成員可以查詢的資料表資料列。 您可以使用 DAX 公式，為模型中的每個資料表定義資料列篩選。  
  
 只有具有「讀取」及「讀取和處理」權限的角色，才可以定義資料列篩選。 根據預設，如果特定資料表未定義資料列篩選，除非從其他資料表套用交叉篩選，否則具有「讀取」或「讀取和處理」權限的角色成員將可以查詢資料表中的所有資料列。  
  
 定義特定資料表的資料列篩選之後，必須評估為 TRUE/FALSE 值的 DAX 公式即會定義該特定角色成員可以查詢的資料列。 無法查詢 DAX 公式中未包含的資料列。 例如，對於 Sales 角色成員，具有下列資料列的 [客戶] 資料表篩選運算式 *= Customers [Country] ="USA"*，Sales 角色成員只能看到美國的客戶。  
  
 資料列篩選會套用至指定的資料列及相關的資料列。 當資料表具有多個關聯性時，篩選會對作用中關聯性套用安全性。 資料列篩選會與針對相關資料表定義的其他資料列篩選進行交叉篩選，例如：  
  
|資料表|DAX 運算式|  
|-----------|--------------------|  
|Region|=Region[Country]="USA"|  
|ProductCategory|=ProductCategory[Name]="Bicycles"|  
|交易|=Transactions[Year]=2008|  
  
 對 Transactions 資料表套用這些權限的結果如下：成員可以查詢美國客戶、自行車產品類別目錄及 2008 年的資料列。 使用者將無法查詢美國以外地區、非自行車及非 2008 年的任何交易，除非成為授與這些權限的其他角色成員。  
  
 您可以使用篩選 ( *=FALSE()*) 拒絕存取整個資料表的所有資料列。  
  
### <a name="dynamic-security"></a>動態安全性  
 動態安全性可根據下列項目來定義資料列層級安全性：目前登入使用者的使用者名稱或從連接字串所傳回的 CustomData 屬性。 若要實作動態安全性，您必須在模型中加入包含使用者登入 (Windows 使用者名稱) 值以及可用來定義特定權限之欄位的資料表，例如具有登入 ID (domain\username) 以及每個員工部門值的 dimEmployees 資料表。  
  
 若要實現動態安全性，您可以使用以下函數做為 DAX 公式的一部分，來傳回目前登入使用者的使用者名稱，或傳回連接字串中的 CustomData 屬性：  
  
|函數|描述|  
|--------------|-----------------|  
|[USERNAME 函式&#40;DAX&#41;](https://msdn.microsoft.com/library/hh230954.aspx)|傳回目前登入使用者的 domain\username。|  
|[CUSTOMDATA 函式&#40;DAX&#41;](https://msdn.microsoft.com/library/hh213140.aspx)|傳回連接字串中的 CustomData 屬性。|  
  
 您可以使用 LOOKUPVALUE 函數傳回資料行值，其中 Windows 使用者名稱與 USERNAME 函數傳回的使用者名稱或 CustomData 函數傳回的字串相同。 然後，可以限制查詢，其中 LOOKUPVALUE 所傳回的值會符合相同或相關資料表中的值。  
  
 例如，使用以下公式：  
  
 `='dimDepartmentGroup'[DepartmentGroupId]=LOOKUPVALUE('dimEmployees'[DepartmentGroupId], 'dimEmployees'[LoginId], USERNAME(), 'dimEmployees'[LoginId], 'dimDepartmentGroup'[DepartmentGroupId])`  
  
 LOOKUPVALUE 函數會傳回 dimEmployees[LoginId] 與 USERNAME 所傳回目前登入使用者的 LoginID 相同，而且 dimEmployees[DepartmentId] 值與 dimDepartmentGroup[DepartmentId] 值相同的 dimEmployees[DepartmentId] 資料行值。 然後，使用 LOOKUPVALUE 所傳回的 DepartmentId 值，來限制 dimDepartment 資料表和依 DepartmentId 相關的任何資料表中查詢的資料列。 只傳回 DepartmentId 值也是 LOOKUPVALUE 函數所傳回 DepartmentId 值的資料列。  
  
 **dimEmployees**  
  
|LastName|FirstName|LoginID|DepartmentName|DepartmentId|  
|--------------|---------------|-------------|--------------------|------------------|  
|Brown|Kevin|Adventure-works\kevin0|Marketing|7|  
|Bradley|David|Adventure-works\david0|Marketing|7|  
|Dobney|JoLynn|Adventure-works\JoLynn0|Production|4|  
|Baretto DeMattos|Paula|Adventure-works\Paula0|Human Resources|2|  
  
 **dimDepartment**  
  
|DepartmentId|DepartmentName|  
|------------------|--------------------|  
|1|Corporate|  
|2|Executive General and Administration|  
|3|Inventory Management|  
|4|Manufacturing|  
|5|Quality Assurance|  
|6|Research and Development|  
|7|Sales and Marketing|  
  
##  <a name="bkmk_testroles"></a> 測試角色  
 在撰寫模型專案時，您可以使用 [在 Excel 中進行分析] 功能，測試所定義之角色的效用。 請從模型設計師中的 **[模型]** 功能表，按一下 **[在 Excel 中進行分析]**， **[選擇認證和檢視方塊]** 對話方塊即會在 Excel 開啟前出現。 在這個對話方塊中，您可指定目前的使用者名稱、其他使用者名稱、角色，以及您想用來連接至做為資料來源之工作空間模型的檢視方塊。 如需詳細資訊，請參閱本主題稍後的 [在 Excel 中進行分析 &#40;SSAS 表格式&#41;](analyze-in-excel-ssas-tabular.md)中的 [角色管理員] 對話方塊來定義角色的表格式模型作者。  
  
##  <a name="bkmk_rt"></a> 相關工作  
  
|主題|描述|  
|-----------|-----------------|  
|[建立及管理角色 &#40;SSAS 表格式&#41;](create-and-manage-roles-ssas-tabular.md)|此主題中的工作描述如何使用 [角色管理員] 對話方塊來建立及管理角色。|  
  
## <a name="see-also"></a>另請參閱  
 [檢視方塊 &#40;SSAS 表格式&#41;](perspectives-ssas-tabular.md)   
 [在 Excel 中進行分析 &#40;SSAS 表格式&#41;](analyze-in-excel-ssas-tabular.md)   
 [USERNAME 函式&#40;DAX&#41;](https://msdn.microsoft.com/library/hh230954.aspx)   
 [LOOKUPVALUE 函式&#40;DAX&#41;](https://msdn.microsoft.com/library/gg492170.aspx)   
 [CUSTOMDATA 函式&#40;DAX&#41;](https://msdn.microsoft.com/library/hh213140.aspx)  
  
  
