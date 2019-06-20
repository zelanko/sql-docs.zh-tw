---
title: 對應 Oracle 和 SQL Server 資料類型 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 06e538ebbdab9d6438182eaa0b61d44818286547
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62796020"
---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>對應 Oracle 和 SQL Server 資料類型 (OracleToSQL)
Oracle 資料庫型別不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫類型。 當您轉換到 Oracle 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件，您必須指定如何將對應從 Oracle 資料型別[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以接受預設資料類型對應，或您可以自訂對應，如下列各節中所示。  
  
## <a name="default-mappings"></a>預設對應  
SSMA 會有一組預設的資料類型對應。 如需預設對應的清單，請參閱[專案設定&#40;類型對應&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)。  
  
## <a name="type-mapping-inheritance"></a>型別對應的繼承  
您可以自訂在專案層級、 物件類別層級 （例如所有預存程序） 或物件層級的型別對應。 從較高的層級會繼承設定，除非它們在較低層級覆寫。 例如，如果您將對應**smallmoney**要**money**在專案層級專案中的所有物件會都使用此對應，除非您自訂物件或類別層級的對應。  
  
當您檢視**型別對應**SSMA，背景中的索引標籤會以色彩標示，顯示繼承的型別對應。 型別對應的背景為黃色任何繼承的型別對應和在目前的層級會指定任何對應的空白的。  
  
## <a name="customizing-data-type-mappings"></a>自訂資料類型對應  
下列程序示範如何在專案、 資料庫或物件層級的資料類型對應：  
  
**若要對應的資料類型**  
  
1.  若要自訂整個專案的資料類型對應，請開啟**專案設定** 對話方塊中：  
  
    1.  在 **工具**功能表上，選取**專案設定**。  
  
    2.  在左窗格中，選取**型別對應**。  
  
        型別對應圖表和按鈕會出現在右窗格中。  
  
    或者，若要自訂資料類型對應在資料庫、 資料表、 檢視或預存程序層級中，選取資料庫、 物件類別或物件 Oracle 中繼資料總管 中：  
  
    1.  在 Oracle 中繼資料總管 中，選取資料夾或自訂的物件。  
  
    2.  在右窗格中，按一下**型別對應** 索引標籤。  
  
2.  若要加入新的對應，請執行下列作業：  
  
    1.  按一下 **[加入]** 。  
  
    2.  底下**來源類型**，選取要對應的 Oracle 資料型別。  
  
    3.  類型需要長度，如果指定的對應中的最小的資料長度**從** 方塊和中的最大資料長度**至** 方塊中。  
  
        這可讓您自訂的資料對應相同的資料類型的較小且較大的值。  
  
    4.  底下**目標型別**，選取目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別。  
  
        某些類型需要目標資料類型長度。 如果需要，請輸入新的資料長度，以**取代為** 方塊中。  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  若要修改的資料類型對應，請執行下列作業：  
  
    1.  按一下 **[編輯]** 。  
  
    2.  底下**來源類型**，選取要對應的 Oracle 資料型別。  
  
    3.  類型需要長度，如果指定的對應中的最小的資料長度**從** 方塊和中的最大資料長度**至** 方塊中。  
  
        這可讓您自訂的資料對應相同的資料類型的較小且較大的值。  
  
    4.  底下**目標型別**，選取目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別。  
  
        某些類型需要目標資料類型長度。 如果需要，請輸入新的資料長度，以**取代為** 方塊中，然後 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  若要移除的自訂資料類型對應，請執行下列作業：  
  
    1.  在包含您想要移除的資料類型對應的類型對應清單中選取的資料列。  
  
    2.  按一下 **[移除]** 。  
  
        您無法移除繼承的對應。 不過，在特定物件或物件類別目錄的自訂對應會覆寫繼承的對應。  
  
## <a name="next-steps"></a>後續步驟  
移轉程序的下一個步驟是為任一[建立評量報告](assessing-oracle-schemas-for-conversion-oracletosql.md)或[將 Oracle 資料庫的物件轉換成 SQL Server 語法](converting-oracle-schemas-oracletosql.md)。 如果您建立的評估報告時，Oracle 物件都會自動轉換評定期間。  
  
## <a name="see-also"></a>另請參閱  
[移轉的 Oracle 資料庫到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
