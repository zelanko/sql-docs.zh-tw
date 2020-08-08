---
title: 將 Oracle 和 SQL Server 資料類型對應 (OracleToSQL) |Microsoft Docs
description: 瞭解如何自訂 Oracle 資料類型與 SQL Server 之間 Oracle 對應的 SSMA，或接受預設值。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 656132dafce39e6007601b75956fd73714638716
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934779"
---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>對應 Oracle 和 SQL Server 資料類型 (OracleToSQL)
Oracle 資料庫類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫類型不同。 當您將 Oracle 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件時，您必須指定如何將資料類型從 Oracle 對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您可以接受預設資料類型對應，也可以自訂對應，如下列各節所示。  
  
## <a name="default-mappings"></a>預設對應  
SSMA 有一組預設的資料類型對應。 如需預設對應的清單，請參閱[專案設定 &#40;類型對應&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)。  
  
## <a name="type-mapping-inheritance"></a>類型對應繼承  
您可以在專案層級、物件類別層級（例如，所有預存程式) 或物件層級）自訂類型對應 (。 設定會繼承自較高的層級，除非它們在較低層級遭到覆寫。 例如，如果您在專案層級將**smallmoney**對應至**money** ，則專案中的所有物件都會使用此對應，除非您在物件或類別層級自訂對應。  
  
當您在 SSMA 中看到 [**型別對應**] 索引標籤時，背景會以色彩標示，以顯示要繼承的型別對應。 任何繼承的型別對應，型別對應的背景都是黃色，而在目前層級指定的任何對應則為白色。  
  
## <a name="customizing-data-type-mappings"></a>自訂資料類型對應  
下列程式顯示如何對應專案、資料庫或物件層級的資料類型：  
  
**對應資料類型**  
  
1.  若要自訂整個專案的資料類型對應，請開啟 [**專案設定**] 對話方塊：  
  
    1.  在 [**工具**] 功能表上，選取 [**專案設定**]。  
  
    2.  在左窗格中，選取 [**類型對應**]。  
  
        類型對應圖表和按鈕會出現在右窗格中。  
  
    或者，若要在資料庫、資料表、視圖或預存程式層級自訂資料類型對應，請在 [Oracle 中繼資料 Explorer] 中選取資料庫、物件類別或物件：  
  
    1.  在 [Oracle 中繼資料 Explorer] 中，選取要自訂的資料夾或物件。  
  
    2.  在右窗格中，按一下 [**類型對應**] 索引標籤。  
  
2.  若要加入新的對應，請執行下列動作：  
  
    1.  按一下 [新增] 。  
  
    2.  在 [**來源類型**] 底下，選取要對應的 Oracle 資料類型。  
  
    3.  如果類型需要長度，請在 [**來源**] 方塊中指定對應的最小資料長度，並在 [**到**] 方塊中指定最大資料長度。  
  
        這可讓您針對相同資料類型的較小且較大的值，自訂資料對應。  
  
    4.  在 [**目標型別**] 底下，選取 [目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型]。  
  
        某些類型需要目標資料類型長度。 如有需要，請在 [**取代為**] 方塊中輸入新的資料長度。  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  若要修改資料類型對應，請執行下列動作：  
  
    1.  按一下 **[編輯]** 。  
  
    2.  在 [**來源類型**] 底下，選取要對應的 Oracle 資料類型。  
  
    3.  如果類型需要長度，請在 [**來源**] 方塊中指定對應的最小資料長度，並在 [**到**] 方塊中指定最大資料長度。  
  
        這可讓您針對相同資料類型的較小且較大的值，自訂資料對應。  
  
    4.  在 [**目標型別**] 底下，選取 [目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型]。  
  
        某些類型需要目標資料類型長度。 如有需要，請在 [**取代為**] 方塊中輸入新的資料長度，然後[!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  若要移除自訂資料類型對應，請執行下列動作：  
  
    1.  選取 [類型對應] 清單中的資料列，其中包含您想要移除的資料類型對應。  
  
    2.  按一下 **[移除]** 。  
  
        您無法移除繼承的對應。 不過，繼承的對應會由特定物件或物件類別上的自訂對應覆寫。  
  
## <a name="next-steps"></a>後續步驟  
遷移程式的下一個步驟是[建立評量報告](assessing-oracle-schemas-for-conversion-oracletosql.md)，或[將 Oracle 資料庫物件轉換成 SQL Server 語法](converting-oracle-schemas-oracletosql.md)。 如果您建立評量報告，Oracle 物件會在評估期間自動轉換。  
  
## <a name="see-also"></a>另請參閱  
[將 Oracle 資料庫移轉至 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
