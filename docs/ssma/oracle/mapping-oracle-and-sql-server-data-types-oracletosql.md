---
title: "Oracle 和 SQL Server 資料類型 (OracleToSQL) 對應 |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 400ed2a28e622ffb9493af7462e06f551a214a51
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>Oracle 和 SQL Server 資料類型 (OracleToSQL) 對應
Oracle 資料庫類型的不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫類型。 當您轉換至 Oracle 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件，您必須指定如何將對應從 Oracle 資料型別[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您可以接受預設資料類型對應，或您可以自訂對應，如下列各節中所示。  
  
## <a name="default-mappings"></a>預設對應  
SSMA 會有一組預設的資料類型對應。 如需預設對應的清單，請參閱[專案設定 &#40;型別對應 &#41;&#40; OracleToSQL &#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
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
  
    或者，若要自訂資料類型對應資料庫、 資料表、 檢視或預存程序層級，在資料庫、 物件類別或物件中選取 Oracle 中繼資料總管:  
  
    1.  在 Oracle 中繼資料總管，選取資料夾或自訂的物件。  
  
    2.  在右窗格中，按一下 [**類型對應**] 索引標籤。  
  
2.  若要加入新的對應，執行下列作業：  
  
    1.  按一下 **[加入]**。  
  
    2.  在下**來源類型**，選取要對應的 Oracle 資料類型。  
  
    3.  如果類型需要長度，指定在對應的最小的資料長度**從**方塊和中的最大資料長度**至**方塊。  
  
        這可讓您自訂為更小且更大的值相同的資料類型的資料對應。  
  
    4.  在下**目標類型**，選取目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
        某些類型需要目標資料類型長度。 如果需要，請輸入新的資料長度，以**取代**方塊。  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
3.  若要修改的資料型別對應，執行下列作業：  
  
    1.  按一下 **[編輯]**。  
  
    2.  在下**來源類型**，選取要對應的 Oracle 資料類型。  
  
    3.  如果類型需要長度，指定在對應的最小的資料長度**從**方塊和中的最大資料長度**至**方塊。  
  
        這可讓您自訂為更小且更大的值相同的資料類型的資料對應。  
  
    4.  在下**目標類型**，選取目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
        某些類型需要目標資料類型長度。 如果需要，請輸入新的資料長度，以**取代** 方塊中，然後按一下[!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
4.  若要移除的自訂資料型別對應，執行下列作業：  
  
    1.  在包含您想要移除的資料類型對應的型別對應清單中選取的資料列。  
  
    2.  按一下 **[移除]**。  
  
        您無法移除繼承的對應。 不過，在特定物件或物件類別目錄的自訂對應會覆寫繼承的對應。  
  
## <a name="next-steps"></a>後續步驟  
移轉程序的下一個步驟是為[建立評估報表](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357)或[將 Oracle 資料庫物件轉換成 SQL Server 語法](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272)。 如果您建立的評估報告時，Oracle 物件會自動轉換期間評估。  
  
## <a name="see-also"></a>另請參閱  
[將 Oracle 資料庫移轉至 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

