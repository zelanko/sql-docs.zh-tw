---
title: 對應 MySQL 和 SQL Server 資料類型 (MySQLToSQL) |Microsoft Docs
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
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 99e86d99a4214b1ccdf317e75218fe22bb2c7af7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908994"
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>對應 MySQL 和 SQL Server 資料類型 (MySQLToSQL)
MySQL 資料庫類型不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 資料庫的型別。 當您將轉換至 MySQL 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 物件，您必須指定如何將資料從 mysql 移轉至的型別對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 您可以接受預設資料類型對應，或您可以自訂對應，如下列程序中所示。  
  
## <a name="default-mappings"></a>預設對應  
SSMA 會有一組預設的資料類型對應。 如需預設對應的清單，請參閱[專案設定&#40;類型對應&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)。  
  
## <a name="type-mapping-inheritance"></a>型別對應的繼承  
您可以自訂在專案層級、 物件類別層級 （例如所有預存程序） 或物件層級的型別對應。 從較高的層級會繼承設定，除非它們在較低層級覆寫。 例如，如果您將對應**smallint**要**int**在專案層級專案中的所有物件會都使用此對應，除非您自訂物件或類別層級的對應。  
  
當您檢視**型別對應**SSMA，背景中的索引標籤會以色彩標示，顯示繼承的型別對應。 型別對應的背景為黃色任何繼承的型別對應和在目前的層級會指定任何對應的空白的。  
  
## <a name="customizing-data-type-mappings"></a>自訂資料類型對應  
  
-   **若要對應的資料類型：**  
  
    下列程序示範如何在專案、 資料庫或資料庫物件層級的資料類型對應：  
  
    1.  若要自訂整個專案的資料類型對應，請開啟**專案設定** 對話方塊。 在 [工具] 功能表中，選取**專案設定**。  
  
        在左窗格中，選取**型別對應**。 型別對應圖表和按鈕會出現在右窗格中。  
  
    2.  若要自訂在資料庫或資料表層級的資料類型對應，請 MySQL 中繼資料總管 中選取資料庫或資料表。 在 [MySQL 中繼資料總管] 中，選取資料夾或自訂的物件。  
  
        在右窗格中，按一下**型別對應**。  
  
-   **若要加入新的對應，請執行下列作業：**  
  
    1.  在類型對應 窗格中，按一下**新增**。  
  
    2.  在 [新增輸入對應] 對話方塊中，下方**來源類型**，選取要對應的 MySQL 資料類型。  
  
    3.  如果類型需要長度，來指定對應的最小和最大資料長度選取**從**並**來**核取方塊，，，然後輸入值。  
  
    4.  這可讓您自訂的資料對應相同的資料類型的較小且較大的值。 底下**目標類型**，選取的目標 SQL Server 或 SQL Azure 的資料型別。  
  
        1.  某些類型需要目標資料類型長度。 如有需要，請輸入新的資料長度，以**取代為**方塊，然後再按一下**確定**。  
  
        2.  某些類型需要的目標資料類型**有效位數**並**擴展**。 如有需要，請輸入新的有效位數和相應縮小**取代為**方塊，然後再按一下**確定**。  
  
-   **若要編輯類型對應，執行下列作業：**  
  
    1.  在類型對應 窗格中，按一下**編輯**。  
  
    2.  中的類型對應清單 對話方塊中，下方**來源類型**，選取要對應的 MySQL 資料類型。  
  
    3.  如果類型需要長度，來指定對應的最小和最大資料長度選取**從**並**來**核取方塊，，，然後輸入值。  
  
    這可讓您自訂的資料對應相同的資料類型的較小且較大的值。 底下**目標類型**，選取的目標 SQL Server 或 SQL Azure 的資料型別。  
  
    1.  某些類型需要目標資料類型長度。 如有需要，請輸入新的資料長度，以**取代為**方塊，然後再按一下**確定**。  
  
    2.  某些類型需要的目標資料類型**有效位數**並**擴展**。 如有需要，請輸入新的有效位數和相應縮小**取代為**方塊，然後再按一下**確定**。  
  
-   **若要移除的資料類型對應，請執行下列作業：**  
  
    1.  在 [類型對應] 窗格中，選取包含您想要移除的資料類型對應的類型對應清單中的資料列。  
  
    2.  按一下 **[移除]** 。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是為任一[建立評量報告](assessing-mysql-databases-for-conversion-mysqltosql.md)或[轉換的 MySQL 資料庫物件為 SQL Server 或 SQL Azure 的語法](converting-mysql-databases-mysqltosql.md)。 如果您建立報表時，評估期間時，會自動轉換 MySQL 物件。  
  
## <a name="see-also"></a>另請參閱  
[移轉 MySQL 資料庫到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
