---
title: 對應 Sybase ASE 和 SQL Server 資料類型 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6400c9ef82a9e787cf818f21d06048c02b1d28f3
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38985320"
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>對應 Sybase ASE 和 SQL Server 資料類型 (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) 的資料庫型別不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫的型別。 當您將轉換至 ASE 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件，您必須指定如何對應資料類型 ASE 能夠從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您可以接受預設資料類型對應，或您可以自訂對應，如下列各節中所示。  
  
## <a name="default-mappings"></a>預設對應  
SSMA 會有一組預設的資料類型對應。 如需預設對應的清單，請參閱[專案設定&#40;類型對應&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)。  
  
## <a name="type-mapping-inheritance"></a>型別對應的繼承  
您可以自訂在專案層級、 物件類別層級 （例如所有預存程序） 或物件層級的型別對應。 除非在較低層級覆寫，會繼承較高層級中設定。 例如，如果您將對應**smallmoney**要**money**在專案層級專案中的所有物件會都使用此對應，除非您自訂的物件類別層級或物件層級的對應。  
  
當您檢視**型別對應**SSMA，背景中的索引標籤會以色彩標示，顯示繼承的型別對應。 型別對應的背景為黃色表示任何繼承的型別對應，並在目前的層級指定任何對應的白色。  
  
## <a name="customizing-data-type-mappings"></a>自訂資料類型對應  
下列程序示範如何在專案、 資料庫或物件層級的資料類型對應。  
  
**若要對應的資料類型**  
  
1.  若要自訂整個專案的資料類型對應，請開啟**專案設定** 對話方塊中：  
  
    1.  在 **工具**功能表上，選取**專案設定**。  
  
    2.  在左窗格中，選取**型別對應**。  
  
        型別對應圖表和按鈕會出現在右窗格中。  
  
    或者，若要自訂資料類型對應，在資料庫、 資料表、 檢視或預存程序層級中，選取資料庫、 物件類別或物件 Sybase 中繼資料總管 中：  
  
    1.  在 Sybase 中繼資料總管 中，選取資料夾或您想要自訂的物件。  
  
    2.  在右窗格中，按一下**型別對應** 索引標籤。  
  
2.  若要加入新的對應，請執行下列作業：  
  
    1.  按一下 **[加入]**。  
  
    2.  底下**來源類型**，選取要對應的 ASE 資料類型。  
  
    3.  如果類型需要長度，指定在對應的最小的資料長度**從**方塊中，並指定在對應的最大資料長度**至** 方塊中。  
  
        這可讓您自訂的資料對應相同的資料類型的較小且較大的值。  
  
    4.  底下**目標型別**，選取目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的資料型別。  
  
        某些類型需要目標資料類型長度。 如果需要，請輸入新的資料長度，以**取代為** 方塊中。  
  
    5.  按一下 [確定] 。  
  
3.  若要編輯的資料類型對應，執行下列作業：  
  
    1.  按一下 **[編輯]**。  
  
    2.  底下**來源類型**，選取要對應的 ASE 資料類型。  
  
    3.  如果類型需要長度，指定在對應的最小的資料長度**從**方塊中，並指定在對應的最大資料長度**至** 方塊中。  
  
        這可讓您自訂的資料對應相同的資料類型的較小且較大的值。  
  
    4.  底下**目標型別**，選取目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的資料型別。  
  
        某些類型需要目標資料類型長度。 如果需要，請輸入新的資料長度，以**取代為**方塊，然後再按一下**確定**。  
  
4.  若要移除的自訂資料類型對應，請執行下列作業：  
  
    1.  在包含您想要移除的資料類型對應的類型對應清單中選取的資料列。  
  
    2.  按一下 **[移除]**。  
  
        您無法移除繼承的對應。 不過，在特定物件或物件類別目錄的自訂對應會覆寫繼承的對應。  
  
## <a name="next-steps"></a>後續步驟  
移轉程序的下一個步驟是為任一[建立評量報告](http://msdn.microsoft.com/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c)或[轉換 Sybase ASE 資料庫物件，SQL Server 或 SQL Azure 的語法](http://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3)。 如果您建立的評估報告，評估期間時，會自動轉換 Sybase ASE 物件。  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
