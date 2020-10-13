---
description: '對應來源和目標資料類型 (AccessToSQL) '
title: 對應來源和目標資料類型 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- customizing data type mappings
- data types, mapping
- mapping, data types
- source data types
- target data types
ms.assetid: b362a075-16e7-423f-b63f-e1e9f02844a9
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 92ce9298b6d3752a4b60e98918404c2116423973
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988674"
---
# <a name="mapping-source-and-target-data-types-accesstosql"></a>對應來源和目標資料類型 (AccessToSQL) 
Access 資料庫類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫類型不同。 當您將 Access 資料庫物件轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件時，您必須指定如何對應資料類型與的存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您可以接受預設資料類型對應，也可以自訂對應，如下列程式所示。  
  
## <a name="default-mappings"></a>預設對應  
SSMA 具有一組預設的資料類型對應。 如需預設對應清單，請參閱 [專案設定 (類型對應) ](./project-settings-type-mapping-accesstosql.md)。  
  
## <a name="customizing-data-type-mappings"></a>自訂資料類型對應  
藉由使用 [ **專案設定** ] 對話方塊，您可以自訂專案中所有資料庫和資料庫物件的對應類型。 專案的類型對應會套用至所有沒有自訂類型對應的資料庫和資料庫物件。  
  
您也可以在資料庫或資料表層級自訂資料類型對應。  
  
下列程式顯示如何對應專案、資料庫或資料庫物件層級的資料類型。  
  
**對應資料類型**  
  
1.  若要自訂整個專案的資料類型對應，請開啟 [ **專案設定** ] 對話方塊：  
  
    1.  在 [ **工具** ] 功能表上，選取 [ **專案設定**]。  
  
    2.  在左窗格中，選取 [ **類型對應**]。  
  
        型別對應圖表和按鈕會出現在右窗格中。  
  
    或者，若要自訂資料庫或資料表層級的資料類型對應，請在 [存取中繼資料瀏覽器] 窗格中選取資料庫或資料表：  
  
    1.  在 [存取中繼資料瀏覽器] 窗格中，展開 [ **存取-元**資料]，然後展開 [ **資料庫**]。  
  
    2.  選取您要自訂資料類型對應的資料庫或資料表。  
  
    3.  在右窗格中，按一下 [ **類型對應**]。  
  
2.  若要加入新的對應，請執行下列動作：  
  
    1.  在 [類型對應] 窗格中，按一下 [ **新增**]。  
  
    2.  在 [ **新增類型對應** ] 對話方塊的 [ **來源類型**] 下，選取要對應的存取資料類型。  
  
    3.  如果類型需要長度，請選取 [ **從** ] 和 [ **至** ] 核取方塊，然後輸入值，以指定對應的最小和最大資料長度。  
  
        這可讓您針對相同資料類型的較小且較大值，自訂資料對應。  
  
    4.  在 [ **目標型別**] 下，選取 [目標] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。  
  
        某些類型需要目標資料類型長度。 如有需要，請在 [ **取代成** ] 方塊中輸入新的資料長度，然後按一下 **[確定]**。  
  
3.  若要編輯資料類型對應，請執行下列動作：  
  
    1.  在 [類型對應] 窗格中，按一下 [ **編輯**]。  
  
    2.  在 [ **類型對應清單** ] 對話方塊的 [ **來源類型**] 下，選取要對應的存取資料類型。  
  
    3.  如果類型需要長度，請選取 [ **從** ] 和 [ **至** ] 核取方塊，然後輸入值，以指定對應的最小和最大資料長度。  
  
        這可讓您針對相同資料類型的較小且較大值，自訂資料對應。  
  
    4.  在 [ **目標型別**] 下，選取 [目標] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。  
  
        某些類型需要目標資料類型長度。 如有需要，請在 [ **取代成** ] 方塊中輸入新的資料長度，然後按一下 **[確定]**。  
  
4.  若要移除資料類型對應，請執行下列動作：  
  
    1.  在 [類型對應] 窗格中，于 [類型對應] 清單中選取包含您要移除之資料類型對應的資料列。  
  
    2.  按一下 **[移除]** 。  
  
## <a name="next-steps"></a>後續步驟  
遷移程式的下一個步驟是 [將 access 資料庫物件轉換成 SQL Server 物件](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
