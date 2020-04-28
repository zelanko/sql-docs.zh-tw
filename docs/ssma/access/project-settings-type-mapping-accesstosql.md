---
title: 專案設定（類型對應）（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 01154cf477435e9dc5335606d0c11a05aecc492b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68066663"
---
# <a name="project-settings-type-mapping-accesstosql"></a>專案設定（類型對應）（AccessToSQL）
[類型對應專案] 設定可讓您設定 SSMA 專案的預設類型對應。 您也可以指定個別資料庫物件的型別對應。 如需詳細資訊，請參閱[對應來源和目標資料類型](mapping-source-and-target-data-types-accesstosql.md)。  
  
在 [**專案設定**] 和 [**預設專案設定**] 對話方塊中，可以使用 [類型對應]：  
  
-   使用 [**專案設定**] 對話方塊，即可設定目前專案的配置選項。 若要存取 [類型對應] 設定，請在 [**工具**] 功能表上選取 [**專案設定**]，然後按一下左窗格中的 [**類型對應**]。  
  
-   使用 [**預設專案設定**] 對話方塊，即可設定所有專案的設定選項。 若要存取型別對應設定，請在 [**工具**] 功能表上，選取 [**預設專案設定**]，從 [**遷移目標版本**] 下拉式下選取需要查看其設定的 [遷移專案類型]/changed，然後按一下左窗格中的 [**類型對應**]。  
  
## <a name="options"></a>選項  
**來源類型**  
要對應的存取資料類型。  
  
**目標型別**  
所指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]存取資料類型的目標或 SQL Azure 資料類型。  
  
下表顯示來源和目標資料類型之間的預設對應。  
  
|存取資料類型|SQL Server 資料類型|  
|--------------------|------------------------|  
|**binary [\*.。\*]**|**Varbinary [\*]**|  
|**boolean**|**bit**|  
|**byte**|**tinyint**|  
|**符號**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**guid**|**uniqueidentifier**|  
|**integer**|**smallint**|  
|**long**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**備忘**|**nvarchar(max)**|  
|**備忘**-適用于存取97|**varchar(max)**|  
|**single**|**real**|  
|**文字 [\*.。\*]**|**Nvarchar [\*]**|  
|**文字 [\*.。] \* ** -用於存取97|**Varchar [\*]**|  
  
**加入**  
按一下即可將資料類型加入至 [對應] 清單。  
  
**編輯**  
按一下即可編輯 [對應] 清單中的資料類型。  
  
**移除**  
按一下即可從 [對應] 清單中移除選取的資料類型對應。  
  
**重設為預設值**  
按一下即可將所有資料類型對應重設為 SSMA 預設值。  
  
## <a name="see-also"></a>另請參閱  
[對應來源和目標資料類型](mapping-source-and-target-data-types-accesstosql.md)  
[使用者介面參考（存取）](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
