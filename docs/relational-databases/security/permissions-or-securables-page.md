---
title: 權限或安全性實體頁面 | Microsoft Docs
description: SQL Server 使用 [權限] 頁面或 [安全性實體] 頁面，以檢視或設定安全性實體的權限。
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.common.permissions.f1
- sql13.swb.SecurableAndEffectPermissions.f1
- sql13.swb.common.columnperm.f1
- sql13.swb.availabilitygroupproperties.permission.f1
- sql13.swb.SecurableAndEffectivePermission.f1
ms.assetid: b3bf077a-bec2-4161-ac0c-460586199906
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a8109779b1afe4badd7c44bd30b264a07503c5fa
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000550"
---
# <a name="permissions-or-securables-page"></a>權限或安全性實體頁面
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  使用 **[權限]** 頁面或 **[安全性實體]** 頁面可檢視或設定安全性實體的權限。 您可以從許多位置開啟此頁面。 此頁面的內容會隨著開啟頁面的方式以及頁面中包含的內容而稍有不同。 當頁面開啟時，頁面的上層方格可能會填入資料或是空白。 若要在上方格中加入項目，請按一下 **[搜尋]** 。 在上方格中選取項目，然後在 **[明確]** 索引標籤上設定適當的權限。若要檢視彙總的權限，請使用 **[有效]** 索引標籤。  
  
 若要了解安全性實體和主體的可能組合，請參閱 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md) 主題中安全性實體特有的語法連結。 如需相關資訊，請參閱 [Securables](../../relational-databases/security/securables.md)。  
  
## <a name="page-header"></a>頁首  
 **[權限]** 或 **[安全性實體]** 頁面的標頭會隨著安全性實體或主體而有所不同。 此頁面顯示項目相關的資訊，例如名稱。  
  
## <a name="upper-grid"></a>上方格  
 上方格包含一或多個可以設定權限的項目。 此對話方塊提供 **[搜尋]** 按鈕，供您選取要加入上方格的物件或主體。 此方格的名稱可能會顯示 **[安全性實體]** 或是安全性實體或主體的一或多個類型。 顯示在上方格中的資料行會隨著主體或安全性實體而有所不同。  
  
 **名稱**  
 加入此方格的每一個主體或安全性實體名稱。  
  
 **型別**  
 描述每個項目的類型。  
  
## <a name="explicit-tab"></a>明確索引標籤  
 **[明確]** 索引標籤會列出上方格中選取之安全性實體的可能權限。 若要設定權限，請選取或清除 [授與] \(或 [允許])、[可授與] 和 [拒絕] 核取方塊。 所有選項不適用於所有明確權限。  
  
 **權限**  
 權限的名稱。  
  
 **授與者**  
 授與權限的主體。  
  
 **授與**  
 選取此選項即可授與此權限給登入。 清除此選項即可撤銷這個權限。  
  
 **使用授與**  
 反映出所列權限之 WITH GRANT 選項的狀態。 這個方塊是唯讀的。 若要套用此權限，請使用 [GRANT](../../t-sql/statements/grant-transact-sql.md) 陳述式。  
  
 **拒絕**  
 選取此選項即可拒絕授與此權限給登入。 清除此選項即可撤銷這個權限。  
  
 **資料行權限**  
 如果是包含資料行的物件 (如資料表、檢視表或資料表值函數)，[資料行權限] 按鈕會開啟 [資料行權限] 對話方塊。 在此對話方塊中，您可以針對資料表或檢視表的個別資料行設定 **[授與]** 、 **[允許]** 或 **[拒絕]** 權限。 並非所有物件類型或權限都可以使用此選項。  
  
## <a name="effective-tab"></a>有效索引標籤  
 主體所擁有而且與安全性實體有關的權限可能來自於針對幾個不同主體所設定的權限。 例如，可個別為登入授與權限，而登入也可以是某個群組的成員。 **[有效]** 索引標籤會顯示結合明確權限以及從群組或角色成員資格取得之權限的結果。 授與的權限會經過彙總。 拒絕權限會覆寫所有授與權限。  
  
 **權限**  
 權限的名稱。  
  
 **資料行**  
 受到權限影響的資料行名稱。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)   
 [SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
