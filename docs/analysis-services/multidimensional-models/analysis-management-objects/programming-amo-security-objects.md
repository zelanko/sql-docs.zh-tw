---
title: "程式設計 AMO 安全性物件 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, security
- AMO, security
ms.assetid: 5d963721-6e6e-46eb-bc9b-18724dd0b751
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 450ae3165942cfdf290a074dd637b220e1c740d8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="programming-amo-security-objects"></a>以程式設計 AMO 安全性物件
  在[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，安全性物件的程式設計或是執行使用 AMO 安全性物件的應用程式需要的伺服器系統管理員群組或資料庫管理員群組的成員。 伺服器管理員與資料庫管理員是存取層級提供[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中，使用者是透過指派給物件的「角色」和「權限」之組合來取得物件的存取權。 如需詳細資訊，請參閱[AMO 安全性類別](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-security-classes.md)。  
  
## <a name="role-and-permission-objects"></a>角色和權限物件  
 伺服器角色在集合中僅包含一個角色：管理員角色。 無法將新角色加入伺服器角色集合。 管理員角色的成員資格允許伺服器內所有物件的完整存取權。  
  
 <xref:Microsoft.AnalysisServices.Role> 物件是在資料庫層級建立。 角色維護只需要在角色中加入或移除成員，以及將角色加入 <xref:Microsoft.AnalysisServices.Database> 物件或是從中卸除。 如果有任何 <xref:Microsoft.AnalysisServices.Permission> 物件與角色關聯，則無法卸除該角色。 若要卸除角色，必須搜尋 <xref:Microsoft.AnalysisServices.Permission> 物件中的所有 <xref:Microsoft.AnalysisServices.Database> 物件，並從權限移除 <xref:Microsoft.AnalysisServices.Role>，才可以從 <xref:Microsoft.AnalysisServices.Role> 卸除 <xref:Microsoft.AnalysisServices.Database>。  
  
 權限會定義獲得權限之物件上的啟用動作。 可以將權限提供到下列物件：<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.DataSource>、<xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.MiningStructure> 和 <xref:Microsoft.AnalysisServices.MiningModel>。 權限的維護包括授與或撤銷對應之存取屬性所啟用的存取。 對於每個啟用的存取，都有一個可以設定成所需存取層級的屬性。 可以針對下列作業定義存取：處理、ReadDefinition、讀取、寫入和管理。 管理存取僅定義於 <xref:Microsoft.AnalysisServices.Database> 物件上。 將管理資料庫的權限授與角色時，便會獲得資料庫管理員安全性層級。  
  
 下列範例會建立四個角色：資料庫管理員、處理器、寫入器和讀取器。  
  
 資料庫管理員可以管理提供的資料庫。  
  
 處理器可以處理資料庫中所有的物件並確認結果。 若要確認結果，必須針對提供的 Cube 明確啟用資料庫物件的讀取存取權，因為讀取權限不會套用到子系物件。  
  
 寫入器可以讀取和寫入提供的 Cube，而且資料格存取權限於客戶維度中的 'United States'。  
  
 讀取器可以讀取提供的 Cube，而且資料格存取權限於客戶維度中的 'United States'。  
  
```  
static public void CreateRolesAndPermissions(Database db, Cube cube)  
{  
    Role role;  
    DatabasePermission dbperm;  
    CubePermission cubeperm;  
  
    #region Create the Database Administrators role  
  
    // Create the Database Administrators role.  
    role = db.Roles.Add("Database Administrators");  
    role.Members.Add(new RoleMember("")); // e.g. domain\user  
    role.Update();  
  
    // Assign administrative permissions to this role.  
    // Members of this role can perform any operation within the database.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Administer = true;  
    dbperm.Update();  
  
    #endregion  
  
    #region Create the Processors role  
  
    // Create the Processors role.  
    role = db.Roles.Add("Processors");  
    role.Members.Add(new RoleMember("")); // e.g. myDomain\johndoe  
    role.Update();  
  
    // Assign Read and Process permissions to this role.  
    // Members of this role can process objects in the database and query them to verify results.  
    // Process permission applies to all contained objects, i.e. all dimensions and cubes.  
    // Read permission does not apply to contained objects, so we must assign the permission explicitly on the cubes.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Process = true;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    cubeperm.Update();  
  
    #endregion  
  
    #region Create the Writers role  
  
    // Create the Writers role.  
    role = db.Roles.Add("Writers");  
    role.Members.Add(new RoleMember("")); // e.g. redmond\johndoe  
    role.Update();  
  
    // Assign Read and Write permissions to this role.  
    // Members of this role can discover, query and writeback to the Adventure Works cube.  
    // However cell access and writeback is restricted to the United States (in the Customer dimension).  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    cubeperm.Write = WriteAccess.Allowed;  
    cubeperm.CellPermissions.Add(new CellPermission(CellPermissionAccess.Read, "[Customer].[Country-Region].CurrentMember is [Customer].[Country-Region].[Country-Region].&[United States]"));  
    cubeperm.CellPermissions.Add(new CellPermission(CellPermissionAccess.ReadWrite, "[Customer].[Country-Region].CurrentMember is [Customer].[Country-Region].[Country-Region].&[United States]"));  
    cubeperm.Update();  
  
    #endregion  
  
    #region Create the Readers role  
  
    // Create the Readers role.  
    role = db.Roles.Add("Readers");  
    role.Members.Add(new RoleMember("")); // e.g. redmond\johndoe  
    role.Update();  
  
    // Assign Read permissions to this role.  
    // Members of this role can discover and query the Adventure Works cube.  
    // However the Customer dimension is restricted to the United States.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    Dimension dim = db.Dimensions.GetByName("Customer");  
    DimensionAttribute attr = dim.Attributes.GetByName("Country-Region");  
    CubeDimensionPermission cubedimperm = cubeperm.DimensionPermissions.Add(dim.ID);  
    cubedimperm.Read = ReadAccess.Allowed;  
    AttributePermission attrperm = cubedimperm.AttributePermissions.Add(attr.ID);  
    attrperm.AllowedSet = "{[Customer].[Country-Region].[Country-Region].&[United States]}";  
    cubeperm.Update();  
  
    #endregion  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices>   
 [AMO 類別簡介](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [程式設計 AMO 安全性物件](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-security-objects.md)   
 [權限和存取權限 &#40;Analysis Services-多維度資料 &#41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [邏輯架構 &#40;Analysis Services-多維度資料 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [資料庫物件 &#40;Analysis Services-多維度資料 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  

