---
title: 對應 MySQL 及 SQL Server 資料類型 (MySQLToSQL) |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping, customize data type mapping
- Mapping, Type mapping
ms.assetid: 14f98054-13b4-4231-a6b0-2452f3b9941d
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 248e908567dfa40f0a8f64596e3f9e9754e03e44
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776504"
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>對應 MySQL 及 SQL Server 資料類型 (MySQLToSQL)
MySQL 資料庫類型的不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫類型。 當您轉換至的 MySQL 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件，您必須指定如何對應資料類型從 MySQL 至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您可以接受預設資料類型對應，或您可以自訂對應，如下列程序中所示。  
  
## <a name="default-mappings"></a>預設對應  
SSMA 會有一組預設的資料類型對應。 如需預設對應的清單，請參閱[專案設定&#40;類型對應&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)。  
  
## <a name="type-mapping-inheritance"></a>型別對應的繼承  
您可以自訂在專案層級、 物件類別層級 （例如所有預存程序） 或物件層級的型別對應。 設定被繼承自較高的層級中，除非它們在較低層級覆寫。 例如，如果您將對應**smallint**至**int**在專案層級專案中的所有物件會都使用此對應，除非您自訂物件或類別層級的對應。  
  
當您檢視**類型對應**SSMA，在背景中的 索引標籤會以色彩標示，以顯示繼承的型別對應。 型別對應的背景為黃色任何繼承的型別對應和目前層級指定任何對應的白色。  
  
## <a name="customizing-data-type-mappings"></a>自訂資料類型對應  
  
-   **若要將資料類型的對應：**  
  
    下列程序顯示如何將對應的專案、 資料庫或資料庫物件層級的資料類型：  
  
    1.  若要自訂整個專案的資料類型對應，請開啟**專案設定** 對話方塊。 在 [工具] 功能表上選取**專案設定**。  
  
        在左窗格中，選取**類型對應**。 型別對應圖表和按鈕會出現在右窗格中。  
  
    2.  若要自訂層級資料庫或資料表的資料類型對應，請選取資料庫或資料表中 MySQL 中繼資料總管。 在 MySQL 中繼資料總管 中，選取資料夾或自訂的物件。  
  
        在右窗格中，按一下 **類型對應**。  
  
-   **若要加入新的對應，執行下列作業：**  
  
    1.  在類型對應 窗格中，按一下**新增**。  
  
    2.  在 [新增輸入對應] 對話方塊底下**來源類型**，選取要對應的 MySQL 資料類型。  
  
    3.  如果類型需要長度，選取以指定對應的最小和最大資料長度**從**和**至**核取方塊，，，然後輸入值。  
  
    4.  這可讓您自訂為更小且更大的值相同的資料類型的資料對應。 在下**目標類型**，選取目標 SQL Server 或 SQL Azure 資料類型。  
  
        1.  某些類型需要目標資料類型長度。 如有需要，請輸入新的資料長度，以**取代為**方塊，然後再按一下**確定**。  
  
        2.  某些類型需要目標資料型別**精確度**和**標尺**。 如有需要，輸入新的有效位數和向內延展**取代為**方塊，然後再按一下**確定**。  
  
-   **若要編輯的型別對應，執行下列作業：**  
  
    1.  在類型對應 窗格中，按一下**編輯**。  
  
    2.  中的類型對應清單對話方塊、 底下**來源類型**，選取要對應的 MySQL 資料類型。  
  
    3.  如果類型需要長度，選取以指定對應的最小和最大資料長度**從**和**至**核取方塊，，，然後輸入值。  
  
    這可讓您自訂為更小且更大的值相同的資料類型的資料對應。 在下**目標類型**，選取目標 SQL Server 或 SQL Azure 資料類型。  
  
    1.  某些類型需要目標資料類型長度。 如有需要，請輸入新的資料長度，以**取代為**方塊，然後再按一下**確定**。  
  
    2.  某些類型需要目標資料型別**精確度**和**標尺**。 如有需要，輸入新的有效位數和向內延展**取代為**方塊，然後再按一下**確定**。  
  
-   **若要移除的資料型別對應，執行下列作業：**  
  
    1.  在類型對應 窗格中，選取包含您想要移除的資料類型對應的型別對應清單中的資料列。  
  
    2.  按一下 **[移除]**。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是為[建立評估報表](http://msdn.microsoft.com/en-us/2a56a003-3b0f-453a-963c-00c9e40933ec)或[轉換 MySQL 資料庫物件為 SQL Server 或 SQL Azure 的語法](http://msdn.microsoft.com/en-us/ac21850b-fb32-4704-9985-5759b7c688c7)。 如果您建立報表時，在評估期間自動轉換 MySQL 物件。  
  
## <a name="see-also"></a>另請參閱  
[移轉的 MySQL 資料庫到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
