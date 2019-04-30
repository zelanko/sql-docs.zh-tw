---
title: 專案設定 （類型對應） (AccessToSQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 8a695217909641c737b7780fc4f8b80b2cb08152
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63299124"
---
# <a name="project-settings-type-mapping-accesstosql"></a>專案設定 （類型對應） (AccessToSQL)
型別對應的專案設定可讓您設定 SSMA 專案的預設型別對應。 您也可以指定個別的資料庫物件的型別對應。 如需詳細資訊，請參閱 <<c0> [ 對應來源和目標資料型別](mapping-source-and-target-data-types-accesstosql.md)。  
  
型別對應可用於**專案設定**並**預設專案設定**對話方塊：  
  
-   使用**專案設定**對話方塊來設定目前專案的組態選項。 若要存取類型的對應設定值，在**工具**功能表上，選取**專案設定**，然後按一下**型別對應**的左窗格中。  
  
-   使用**預設專案設定**對話方塊來設定的所有專案的組態選項。 若要存取類型的對應設定值，在**工具**功能表上，選取**預設專案設定**，選取 移轉專案類型，則需要檢視 / 變更設定**移轉目標版本**下拉式清單，然後再按**型別對應**的左窗格中。  
  
## <a name="options"></a>選項。  
**來源類型**  
存取的資料類型對應。  
  
**目標類型**  
目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或指定的存取資料類型的 SQL Azure 資料型別。  
  
下表顯示來源和目標資料類型之間的預設對應。  
  
|存取資料類型|SQL Server 資料類型|  
|--------------------|------------------------|  
|**binary[\*..\*]**|**varbinary[\*]**|  
|**boolean**|**bit**|  
|**byte**|**tinyint**|  
|**currency**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**guid**|**uniqueidentifier**|  
|**integer**|**smallint**|  
|**long**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**memo**|**nvarchar(max)**|  
|**備忘錄**-適用於 Access 97|**varchar(max)**|  
|**single**|**real**|  
|**text[\*..\*]**|**nvarchar[\*]**|  
|**text[\*..\*]** - for Access 97|**varchar[\*]**|  
  
**[加入]**  
按一下以新增的資料類型對應清單。  
  
**編輯**  
按一下以編輯 [對應] 清單中的資料類型。  
  
**移除**  
按一下即可從對應清單中移除選取的資料類型對應。  
  
**重設為預設值**  
按一下以重設為 SSMA 預設值的所有資料類型對應。  
  
## <a name="see-also"></a>另請參閱  
[對應來源和目標資料類型](mapping-source-and-target-data-types-accesstosql.md)  
[使用者介面 Reference(Access)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
