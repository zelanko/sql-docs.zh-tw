---
title: "專案設定 （型別對應） (AccessToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
caps.latest.revision: "16"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1d82b431499de3986f0358074ad96e4acc69fb41
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="project-settings-type-mapping-accesstosql"></a>專案設定 （型別對應） (AccessToSQL)
型別對應的專案設定可讓您設定的 SSMA 專案的預設型別對應。 您也可以指定個別的資料庫物件的型別對應。 如需詳細資訊，請參閱[對應來源和目標資料型別](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)。  
  
型別對應是用於**專案設定**和**預設專案設定**對話方塊：  
  
-   使用**專案設定**對話方塊來設定目前專案的組態選項。 若要存取的型別對應設定，在**工具**功能表上，選取**專案設定**，然後按一下 **型別對應**的左窗格中。  
  
-   使用**預設專案設定**對話方塊來設定所有專案的組態選項。 若要存取的型別對應設定，在**工具**功能表上，選取**預設專案設定**，選取移轉專案類型設定為需要從變更 / 檢視**移轉的目標版本**下拉式清單，然後按一下 **型別對應**的左窗格中。  
  
## <a name="options"></a>選項。  
**來源類型**  
存取的資料類型對應。  
  
**目標類型**  
目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的資料類型的指定存取資料型別。  
  
下表顯示來源和目標資料類型之間的預設對應。  
  
|存取資料類型|SQL Server 資料類型|  
|--------------------|------------------------|  
|**二進位 [\*..\*]**|**varbinary [\*]**|  
|**boolean**|**bit**|  
|**位元組**|**tinyint**|  
|**貨幣**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**guid**|**uniqueidentifier**|  
|**integer**|**smallint**|  
|**長**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**附註**|**nvarchar(max)**|  
|**備忘**： 適用於 Access 97|**varchar(max)**|  
|**單一**|**real**|  
|**text[\*..\*]**|**nvarchar [\*]**|  
|**text[\*..\*]** ： 適用於 Access 97|**varchar [\*]**|  
  
**加入**  
按一下以新增的資料類型對應清單。  
  
**編輯**  
按一下以編輯對應清單中的資料類型。  
  
**移除**  
按一下即可從對應清單中移除選取的資料類型對應。  
  
**重設預設值**  
按一下以重設 SSMA 的所有資料類型對應。  
  
## <a name="see-also"></a>請參閱  
[對應來源和目標資料類型](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)  
[使用者介面 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
