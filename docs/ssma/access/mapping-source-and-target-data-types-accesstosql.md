---
title: 對應來源和目標資料類型 (AccessToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
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
- customizing data type mappings
- data types, mapping
- mapping, data types
- source data types
- target data types
ms.assetid: b362a075-16e7-423f-b63f-e1e9f02844a9
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3bb6bd72d6b20ef207653b904607a9df942c2858
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-source-and-target-data-types-accesstosql"></a>對應來源和目標資料類型 (AccessToSQL)
存取資料庫類型的不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫類型。 當您轉換到存取資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件，您必須指定如何將存取權的資料類型對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您可以接受預設資料類型對應，或您可以自訂對應，如下列程序中所示。  
  
## <a name="default-mappings"></a>預設對應  
SSMA 會有一組預設的資料類型對應。 如需預設對應的清單，請參閱[（型別對應） 的專案設定](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655)。  
  
## <a name="customizing-data-type-mappings"></a>自訂資料類型對應  
使用**專案設定**對話方塊中，您可以自訂如何所有資料庫和資料庫物件，在專案中的對應型別。 專案的類型對應套用至所有資料庫和資料庫物件不具有自訂類型對應。  
  
您也可以自訂層級資料庫或資料表的資料類型對應。  
  
下列程序示範如何將在專案、 資料庫或資料庫物件層級的資料類型對應。  
  
**若要將資料類型對應**  
  
1.  若要自訂整個專案的資料類型對應，請開啟**專案設定**對話方塊：  
  
    1.  在**工具**功能表上，選取**專案設定**。  
  
    2.  在左窗格中，選取**類型對應**。  
  
        型別對應圖表和按鈕會出現在右窗格中。  
  
    或者，若要自訂層級資料庫或資料表的資料類型對應，在存取中繼資料總管 窗格中選取資料庫或資料表：  
  
    1.  在存取中繼資料總管] 窗格中，展開 [**存取 metabase**，然後展開**資料庫**。  
  
    2.  選取您要自訂的資料類型對應的資料庫或資料表。  
  
    3.  在右窗格中，按一下 **類型對應**。  
  
2.  若要加入新的對應，執行下列作業：  
  
    1.  在類型對應 窗格中，按一下**新增**。  
  
    2.  在**新類型對應**對話方塊的 **來源類型**，選取要對應的存取資料類型。  
  
    3.  如果類型需要長度，選取以指定對應的最小和最大資料長度**從**和**至**核取方塊，，，然後輸入值。  
  
        這可讓您自訂為更小且更大的值相同的資料類型的資料對應。  
  
    4.  在下**目標類型**，選取目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
        某些類型需要目標資料類型長度。 如果需要，請輸入新的資料長度，以**取代為**方塊，然後再按一下**確定**。  
  
3.  若要編輯的資料型別對應，執行下列作業：  
  
    1.  在類型對應 窗格中，按一下**編輯**。  
  
    2.  在**類型對應清單**對話方塊的 **來源類型**，選取要對應的存取資料類型。  
  
    3.  如果類型需要長度，選取以指定對應的最小和最大資料長度**從**和**至**核取方塊，，，然後輸入值。  
  
        這可讓您自訂為更小且更大的值相同的資料類型的資料對應。  
  
    4.  在下**目標類型**，選取目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
        某些類型需要目標資料類型長度。 如果需要，請輸入新的資料長度，以**取代為**方塊，然後再按一下**確定**。  
  
4.  若要移除的資料型別對應，執行下列作業：  
  
    1.  在類型對應 窗格中，選取包含您想要移除的資料類型對應的型別對應清單中的資料列。  
  
    2.  按一下 **[移除]**。  
  
## <a name="next-steps"></a>後續步驟  
移轉程序的下一個步驟是[將存取資料庫物件轉換為 SQL Server 物件](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
