---
title: 角色 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 507c5f0d6e610113082a1c1b6cc1d5f971672a09
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="roles"></a>角色
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  表格式模型中的角色定義模型的成員權限。 角色的成員可以依角色權限所定義，對模型執行動作。 以讀取權限定義的角色也可以使用資料列層級篩選，在資料列層級提供額外的安全性。 
  
 SQL Server Analysis services，角色包含使用者成員依 Windows 使用者名稱或 Windows 群組和權限 （讀取、 處理程序、 系統管理員）。 Azure Analysis services，使用者必須在您的 Azure Active Directory 和使用者名稱和指定的群組都必須是組織的電子郵件地址的 UPN。 
  
> [!IMPORTANT]  
>  讓使用者使用報表用戶端應用程式連接到已部署的模型，您必須至少建立至少一個角色具有讀取權限的使用者都是成員。  
  
 本主題資訊適用於使用 SSDT 中的 [角色管理員] 對話方塊來定義角色的表格式模型作者。 在模型製作期間定義的角色會套用至模型工作空間資料庫。 部署模型資料庫之後，模型資料庫管理員可以管理 （加入、 編輯、 刪除） 角色成員使用 SSMS。 若要了解如何管理已部署的資料庫中角色的成員，請參閱[表格式模型角色](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md)。  
  
##  <a name="bkmk_underst"></a> Understanding roles  
 Analysis Services 中使用角色來管理模型資料存取。 目前有兩種角色類型：  
  
-   伺服器角色、 固定的角色，提供系統管理員存取權的 Analysis Services 伺服器執行個體。  
  
-   資料庫角色，這是模型作者和管理員所定義的角色，用來控制非管理員使用者對模型資料庫和資料的存取。  
  
 針對表格式模型定義的角色就是資料庫角色。 也就是說，這些角色的成員組成的使用者或群組，那些成員已經定義動作的特定權限可在模型資料庫上。 資料庫角色會建立成資料庫中的個別物件，且只適用於建立該角色的資料庫。 使用者和群組包含在角色中由模型作者，可以根據預設，工作空間資料庫伺服器中，具有系統管理權限已部署的模型，由系統管理員。  
  
 表格式模型中的角色可以進一步透過資料列篩選定義。 資料列篩選使用 DAX 運算式定義使用者可以查詢的資料表資料列，以及許多方向的任何相關資料列。 只有「讀取」及「讀取和處理」權限，才可以定義使用 DAX 運算式的資料列篩選。 若要進一步了解，請參閱[資料列篩選器](#bkmk_rowfliters)本主題稍後。  
  
 根據預設，當您建立新的表格式模型專案時，模型專案沒有任何角色。 角色可以使用 SSDT 中的 [角色管理員] 對話方塊來定義。 在模型撰寫期間定義角色時，會將這些角色套用至模型工作空間資料庫。 部署模型時，會將相同的角色套用至已部署的模型。 在部署模型之後，伺服器角色 （[Analysis Services 系統管理員） 和資料庫管理員的成員可以管理與模型相關聯的角色以及使用 SSMS 相關聯的每個角色的成員。  
  
##  <a name="bkmk_permissions"></a> Permissions  
 每一個角色都有一個已定義的資料庫權限 (但不包括「讀取和處理」結合權限)。 新角色的預設權限為「無」。 換句話說，成員一旦加入至具有「無」權限的角色後，除非授與其他權限，否則將無法修改資料庫、執行處理作業、查詢資料或查看資料庫。  
  
 群組或使用者可以是任意數目的角色，每個具有不同的權限的角色成員。 當使用者是多個角色的成員時，針對每個角色定義的權限會累計。 例如，如果某位使用者是具有「讀取」權限之角色的成員，同時也是具有「無」權限之角色的成員，則該使用者將具有「讀取」權限。  
  
 每個角色可以定義下列其中一個權限：  
  
|Permissions|Description|使用 DAX 的資料列篩選|  
|-----------------|-----------------|----------------------------|  
|無|成員無法對模型資料庫結構描述進行任何修改，也無法查詢資料。|不會套用資料列篩選。 此角色的使用者看不到任何資料|  
|讀取|允許成員查詢資料 (根據資料列篩選)，但是無法在 SSMS 中看到模型資料庫，也無法對模型資料庫結構描述做任何變更，使用者也無法處理模型。|可套用資料列篩選。 使用者只能看到資料列篩選 DAX 公式中指定的資料。|  
|讀取和處理|成員可以查詢資料 (根據資料列層級篩選)，並透過執行指令碼或包含處理命令的封裝來執行處理作業，但無法對資料庫進行任何變更。 無法在 SSMS 中檢視模型資料庫。|可套用資料列篩選。 只能查詢資料列篩選 DAX 公式中指定的資料。|  
|處理|成員可以透過執行指令碼或包含處理命令的封裝來執行處理作業。 無法修改模型資料庫結構描述。 無法查詢資料。 無法查詢在 SSMS 中的模型資料庫。|不會套用資料列篩選。 無法查詢此角色中的任何資料|  
|系統管理員|成員可以對模型結構描述進行修改，也可以查詢模型設計師、 報表用戶端和 SSMS 中的所有資料。|不會套用資料列篩選。 可以查詢此角色中的所有資料。|  
  
##  <a name="bkmk_rowfliters"></a> Row filters  
 資料列篩選會定義特定角色的成員可以查詢的資料表資料列。 您可以使用 DAX 公式，為模型中的每個資料表定義資料列篩選。  
  
 只有具有「讀取」及「讀取和處理」權限的角色，才可以定義資料列篩選。 根據預設，如果特定資料表未定義資料列篩選，除非從其他資料表套用交叉篩選，否則具有「讀取」或「讀取和處理」權限的角色成員將可以查詢資料表中的所有資料列。  
  
 定義特定資料表的資料列篩選之後，必須評估為 TRUE/FALSE 值的 DAX 公式即會定義該特定角色成員可以查詢的資料列。 無法查詢 DAX 公式中未包含的資料列。 例如，對於 Sales 角色成員來說 (具有下列資料列篩選運算式 *=Customers [Country] = “USA”*的 Customers 資料表)，Sales 角色成員只能看到美國的客戶。  
  
 資料列篩選會套用至指定的資料列及相關的資料列。 當資料表具有多個關聯性時，篩選會對作用中關聯性套用安全性。 資料列篩選會與針對相關資料表定義的其他資料列篩選進行交叉篩選，例如：  
  
|Table|DAX 運算式|  
|-----------|--------------------|  
|Region|=Region[Country]=”USA”|  
|ProductCategory|=ProductCategory[Name]=”Bicycles”|  
|交易|=Transactions[Year]=2008|  
  
 對 Transactions 資料表套用這些權限的結果如下：成員可以查詢美國客戶、自行車產品類別目錄及 2008 年的資料列。 使用者將無法查詢美國以外地區、非自行車及非 2008 年的任何交易，除非成為授與這些權限的其他角色成員。  
  
 您可以使用篩選 ( *=FALSE()*) 拒絕存取整個資料表的所有資料列。  
  
### <a name="dynamic-security"></a>動態安全性  
 動態安全性可根據下列項目來定義資料列層級安全性：目前登入使用者的使用者名稱或從連接字串所傳回的 CustomData 屬性。 若要實作動態安全性，您必須在模型中加入包含使用者登入 (Windows 使用者名稱) 值以及可用來定義特定權限之欄位的資料表，例如具有登入 ID (domain\username) 以及每個員工部門值的 dimEmployees 資料表。  
  
 若要實現動態安全性，您可以使用以下函數做為 DAX 公式的一部分，來傳回目前登入使用者的使用者名稱，或傳回連接字串中的 CustomData 屬性：  
  
|函數|Description|  
|--------------|-----------------|  
|[USERNAME 函數 (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f)|傳回目前登入使用者的 domain\username。|  
|[CUSTOMDATA 函數 (DAX)](http://msdn.microsoft.com/en-us/58235ad8-226c-43cc-8a69-5a52ac19dd4e)|傳回連接字串中的 CustomData 屬性。|  
  
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
  
##  <a name="bkmk_testroles"></a> Testing roles  
 在撰寫模型專案時，您可以使用 [在 Excel 中進行分析] 功能，測試所定義之角色的效用。 請從模型設計師中的 **[模型]** 功能表，按一下 **[在 Excel 中進行分析]**， **[選擇認證和檢視方塊]** 對話方塊即會在 Excel 開啟前出現。 在這個對話方塊中，您可指定目前的使用者名稱、其他使用者名稱、角色，以及您想用來連接至做為資料來源之工作空間模型的檢視方塊。 若要進一步了解，請參閱[在 Excel 中的進行分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)。  
  
##  <a name="bkmk_rt"></a> Related tasks  
  
|主題|Description|  
|-----------|-----------------|  
|[建立及管理角色](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)|此主題中的工作描述如何使用 [角色管理員] 對話方塊來建立及管理角色。|  
  
## <a name="see-also"></a>另請參閱  
 [檢視方塊](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [在 Excel 中進行分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)   
 [USERNAME 函數 (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f)   
 [LOOKUPVALUE 函數 (DAX)](http://msdn.microsoft.com/en-us/73a51c4d-131c-4c33-a139-b1342d10caab)   
 [CUSTOMDATA 函數 (DAX)](http://msdn.microsoft.com/en-us/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
  
  
