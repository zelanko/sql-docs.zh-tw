---
title: 對應 DB2 與 SQL Server 資料類型 (DB2ToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
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
ms.assetid: e7e939a8-5e76-4509-beaf-5acd1cab505e
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: dfee3ae96aadbb2f498b605aaacc818d96ce60a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-db2-and-sql-server-data-types-db2tosql"></a>對應 DB2 與 SQL Server 資料類型 (DB2ToSQL)
DB2 資料庫類型的不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫類型。 當您轉換至 DB2 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件，您必須指定如何對應到 DB2 中的資料類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您可以接受預設資料類型對應，或您可以自訂對應，如下列各節中所示。  
  
## <a name="default-mappings"></a>預設對應  
SSMA 會有一組預設的資料類型對應。 如需預設對應的清單，請參閱[專案設定&#40;類型對應&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)。  
  
## <a name="type-mapping-inheritance"></a>型別對應的繼承  
您可以自訂在專案層級、 物件類別層級 （例如所有預存程序） 或物件層級的型別對應。 設定被繼承自較高的層級中，除非它們在較低層級覆寫。 例如，如果您將對應**smallmoney**至**money**在專案層級專案中的所有物件會都使用此對應，除非您自訂物件或類別層級的對應。  
  
當您檢視**類型對應**SSMA，在背景中的 索引標籤會以色彩標示，以顯示繼承的型別對應。 型別對應的背景為黃色任何繼承的型別對應和目前層級指定任何對應的白色。  
  
## <a name="customizing-data-type-mappings"></a>自訂資料類型對應  
下列程序示範如何將對應的專案、 資料庫或物件層級的資料類型：  
  
**若要將資料類型對應**  
  
1.  若要自訂整個專案的資料類型對應，請開啟**專案設定**對話方塊：  
  
    1.  在**工具**功能表上，選取**專案設定**。  
  
    2.  在左窗格中，選取**類型對應**。  
  
        型別對應圖表和按鈕會出現在右窗格中。  
  
    或者，若要自訂資料類型對應，在資料庫、 資料表、 檢視或預存程序層級，選取資料庫、 物件類別或物件中 DB2 中繼資料總管:  
  
    1.  在 DB2 中繼資料總管，選取資料夾或自訂的物件。  
  
    2.  在右窗格中，按一下 [**類型對應**] 索引標籤。  
  
2.  若要加入新的對應，執行下列作業：  
  
    1.  按一下 **[加入]**。  
  
    2.  在下**來源類型**，選取要對應的 DB2 資料類型。  
  
    3.  如果類型需要長度，指定在對應的最小的資料長度**從**方塊和中的最大資料長度**至**方塊。  
  
        這可讓您自訂為更小且更大的值相同的資料類型的資料對應。  
  
    4.  在下**目標類型**，選取目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
        某些類型需要目標資料類型長度。 如果需要，請輸入新的資料長度，以**取代**方塊。  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
3.  若要修改的資料型別對應，執行下列作業：  
  
    1.  按一下 **[編輯]**。  
  
    2.  在下**來源類型**，選取要對應的 DB2 資料類型。  
  
    3.  如果類型需要長度，指定在對應的最小的資料長度**從**方塊和中的最大資料長度**至**方塊。  
  
        這可讓您自訂為更小且更大的值相同的資料類型的資料對應。  
  
    4.  在下**目標類型**，選取目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
        某些類型需要目標資料類型長度。 如果需要，請輸入新的資料長度，以**取代** 方塊中，然後按一下 [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
4.  若要移除的自訂資料型別對應，執行下列作業：  
  
    1.  在包含您想要移除的資料類型對應的型別對應清單中選取的資料列。  
  
    2.  按一下 **[移除]**。  
  
        您無法移除繼承的對應。 不過，在特定物件或物件類別目錄的自訂對應會覆寫繼承的對應。  
  
## <a name="next-steps"></a>後續步驟  
移轉程序的下一個步驟是為[評估報表&#40;DB2ToSQL&#41; ](../../ssma/db2/assessment-report-db2tosql.md)或[轉換 DB2 結構描述&#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)。 如果您建立的評估報告，評估期間自動轉換 DB2 物件。  
  
## <a name="see-also"></a>另請參閱  
[SQL server 資料庫移轉 DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
