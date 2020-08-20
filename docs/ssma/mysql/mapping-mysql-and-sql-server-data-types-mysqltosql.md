---
description: 對應 MySQL 和 SQL Server 資料類型 (MySQLToSQL)
title: 將 MySQL 和 SQL Server 資料類型對應 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, customize data type mapping
- Mapping, Type mapping
ms.assetid: 14f98054-13b4-4231-a6b0-2452f3b9941d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 0df267807ff824cebac580fb3454d63de8dfe31b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463381"
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>對應 MySQL 和 SQL Server 資料類型 (MySQLToSQL)
MySQL 資料庫類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 類型不同。 當您將 MySQL 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Sql azure 物件時，您必須指定如何將 mysql 的資料類型對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 sql azure。 您可以接受預設資料類型對應，也可以自訂對應，如下列程式所示。  
  
## <a name="default-mappings"></a>預設對應  
SSMA 具有一組預設的資料類型對應。 如需預設對應清單，請參閱 [&#40;類型對應的專案設定&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)。  
  
## <a name="type-mapping-inheritance"></a>類型對應繼承  
您可以在專案層級、物件類別層級 (（例如所有預存程式) 或物件層級）自訂類型對應。 除非在較低層級覆寫設定，否則設定會繼承自較高的層級。 例如，如果您將 **Smallint** 對應到專案層級的 **int** ，除非您自訂物件或類別層級的對應，否則專案中的所有物件都會使用此對應。  
  
當您在 SSMA 中查看 [ **類型對應** ] 索引標籤時，背景會以色彩標示，以顯示要繼承的類型對應。 類型對應的背景為黃色，表示任何繼承的型別對應，以及在目前層級指定之任何對應的白色。  
  
## <a name="customizing-data-type-mappings"></a>自訂資料類型對應  
  
-   **若要對應資料類型：**  
  
    下列程式顯示如何對應專案、資料庫或資料庫物件層級的資料類型：  
  
    1.  若要自訂整個專案的資料類型對應，請開啟 [ **專案設定** ] 對話方塊。 在 [工具] 功能表上，選取 [ **專案設定**]。  
  
        在左窗格中，選取 [ **類型對應**]。 型別對應圖表和按鈕會出現在右窗格中。  
  
    2.  若要自訂資料庫或資料表層級的資料類型對應，請選取 MySQL 中繼資料瀏覽器中的資料庫或資料表。 在 MySQL 中繼資料瀏覽器中，選取要自訂的資料夾或物件。  
  
        在右窗格中，按一下 [ **類型對應**]。  
  
-   **若要加入新的對應，請執行下列動作：**  
  
    1.  在 [類型對應] 窗格中，按一下 [ **新增** ]。  
  
    2.  在 [新增類型對應] 對話方塊的 [ **來源類型**] 下，選取要對應的 MySQL 資料類型。  
  
    3.  如果類型需要長度，請選取 [ **從** ] 和 [ **至** ] 核取方塊，然後輸入值，以指定對應的最小和最大資料長度。  
  
    4.  這可讓您針對相同資料類型的較小且較大值，自訂資料對應。 在 [ **目標型別**] 下，選取 [目標 SQL Server] 或 [SQL Azure] 資料類型。  
  
        1.  某些類型需要目標資料類型長度。 如有需要，請在 [ **取代成** ] 方塊中輸入新的資料長度，然後按一下 **[確定]**。  
  
        2.  某些類型需要目標資料類型的**precision**有效**位數和小**數位數。 如有需要，請在 [ **取代成** ] 方塊中輸入新的有效位數和小數位數，然後按一下 **[確定]**。  
  
-   **若要編輯類型對應，請執行下列動作：**  
  
    1.  在 [類型對應] 窗格中，按一下 [ **編輯**]。  
  
    2.  在 [類型對應清單] 對話方塊的 [ **來源類型**] 下，選取要對應的 MySQL 資料類型。  
  
    3.  如果類型需要長度，請選取 [ **從** ] 和 [ **至** ] 核取方塊，然後輸入值，以指定對應的最小和最大資料長度。  
  
    這可讓您針對相同資料類型的較小且較大值，自訂資料對應。 在 [ **目標型別**] 下，選取 [目標 SQL Server] 或 [SQL Azure] 資料類型。  
  
    -  某些類型需要目標資料類型長度。 如有需要，請在 [ **取代成** ] 方塊中輸入新的資料長度，然後按一下 **[確定]**。  
  
    -  某些類型需要目標資料類型的**precision**有效**位數和小**數位數。 如有需要，請在 [ **取代成** ] 方塊中輸入新的有效位數和小數位數，然後按一下 **[確定]**。  
  
-   **若要移除資料類型對應，請執行下列動作：**  
  
    1.  在 [類型對應] 窗格中，于 [類型對應] 清單中選取包含您要移除之資料類型對應的資料列。  
  
    2.  按一下 **[移除]** 。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是 [建立評定報告](assessing-mysql-databases-for-conversion-mysqltosql.md) ，或 [將 MySQL 資料庫物件轉換成 SQL Server 或 SQL Azure 語法](converting-mysql-databases-mysqltosql.md)。 如果您建立報表，則會在評估期間自動轉換 MySQL 物件。  
  
## <a name="see-also"></a>另請參閱  
[將 MySQL 資料庫遷移至 SQL Server Azure SQL Database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
