---
title: "專案設定 （型別對應） (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 77c02b875a22fefec54c59518f4972cbd7aefd4b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-type-mapping-sybasetosql"></a>專案設定 （型別對應） (SybaseToSQL)
類型對應 頁面**專案設定**對話方塊包含自訂 SSMA 如何轉換成 Sybase Adaptive Server Enterprise (ASE) 資料類型的設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
型別對應的頁面位於**專案設定**和**預設專案設定**對話方塊。  
  
-   若要指定的型別對應設定為所有未來的 SSMA 專案，在**工具**功能表上，選取**預設專案設定**，選取移轉專案類型，不需要檢視或變更設定**移轉的目標版本**下拉式清單，然後選取**型別對應**在左窗格的底部。  
  
-   若要指定目前的專案中，設定**工具**功能表上，選取**專案設定**，然後選取**類型對應**在左窗格底部。  
  
## <a name="options"></a>選項  
**來源類型**  
對應的 ASE 資料類型。  
  
**目標類型**  
目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]指定 ASE 資料類型的資料類型。  
  
請參閱下節以取得預設 SSMA for Sybase 型別對應中的資料表。  
  
**加入**  
按一下以新增的資料類型對應清單。  
  
**編輯**  
按一下以編輯選取的資料類型對應清單中。  
  
**移除**  
按一下即可從對應清單中移除選取的資料類型對應。  
  
**重設預設值**  
按一下 重設為 SSMA 預設值的類型對應清單。  
  
## <a name="default-type-mapping"></a>預設型別對應  
下表包含 ASE 之間的預設型別對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
|ASE 資料類型|SQL Server 資料類型|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**二進位 [\*..8000]**|**二進位 [\*]**|  
|**二進位 [8001..\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**char varying [\*..8000]**|**varchar [\*]**|  
|**char varying [8001..\*]**|**varchar(max)**|  
|**char[\*..8000]**|**char[\*]**|  
|**char [8001..\&# 42;]**|**varchar(max)**|  
|**字元**|**char**|  
|**可變長度字元**|**varchar**|  
|**可變長度字元 [\*..8000]**|**varchar [\*]**|  
|**可變長度字元 [8001..\*]**|**varchar(max)**|  
|**字元 [\*..8000]**|**char[\*]**|  
|**字元 [8001..\*]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2 [3]**|  
|**dec**|**decimal**|  
|**dec[\*..\*]**|**小數 [\*]**|  
|**dec[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**小數 [\*..\*]**|**小數 [\*]**|  
|**小數 [\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**雙精度**|**float [53]**|  
|**float**|**float [53]**|  
|**float [\*..15]**|**float [24]**|  
|**float [16..\*]**|**float [53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**nvarchar [255]**|  
|**money**|**money**|  
|**國家 （地區) 的 char**|**nchar**|  
|**國家 （地區) 的 char [\*..4000]**|**nchar [\*]**|  
|**不同國家 （地區) 的 char**|**nvarchar**|  
|**不同國家 （地區) 的 char [\*..4000]**|**nvarchar [\*]**|  
|**不同國家 （地區) 的 char [4001..\*]**|**nvarchar(max)**|  
|**國家 （地區) 的 char [4001..\*]**|**nvarchar(max)**|  
|**國家字元集**|**nchar**|  
|**國家字元集 [\*..4000]**|**nchar [\*]**|  
|**國家字元集 [4001..\*]**|**nvarchar(max)**|  
|**不同的國家字元集**|**nvarchar**|  
|**不同的國家字元集 [\*..4000]**|**nvarchar [\*]**|  
|**不同的國家字元集 [4001..\*]**|**nvarchar(max)**|  
|**國家 （地區) 的 varchar**|**nvarchar**|  
|**國家 （地區) 的 varchar [\*..4000]**|**nvarchar [\*]**|  
|**國家 （地區) 的 varchar [4001..\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar 變動**|**nvarchar**|  
|**nchar 變動 [\*..4000]**|**nvarchar [\*]**|  
|**nchar 變動 [4001..\*]**|**nvarchar(max)**|  
|**nchar [\*..4000]**|**nchar [\*]**|  
|**nchar [4001..\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**數字 [\*..\*]**|**數字 [\*]**|  
|**數字 [\*..\*][\*..\*]**|**numeric[\*][\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar [\*..4000]**|**nvarchar [\*]**|  
|**nvarchar [4001..\*]**|**nvarchar(max)**|  
|**real**|**float [24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar [128]**|  
|**sysname [\*..\*]**|**nvarchar [255]**|  
|**text**|**text**|  
|**time**|**時間 [3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**unichar 變動**|**nvarchar**|  
|**unichar 變動 [\*..4000]**|**nvarchar [\*]**|  
|**unichar 變動 [4001..\*]**|**nvarchar(max)**|  
|**unichar [\*..4000]**|**nchar [\*]**|  
|**unichar [4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar [\*..4000]**|**nvarchar [\*]**|  
|**univarchar [4001..\*]**|**nvarchar(max)**|  
|**不帶正負號的 bigint**|**數字 [20] [0]**|  
|**不帶正負號的 int**|**bigint**|  
|**不帶正負號的 smallint**|**int**|  
|**不帶正負號的 tinyint**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary [\*..8000]**|**varbinary [\*]**|  
|**varbinary [8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar [\*..8000]**|**varchar [\*]**|  
|**varchar [8001..\*]**|**varchar(max)**|  
  

