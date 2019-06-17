---
title: 專案設定 （類型對應） (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 148180d95bcbff1626069e72fb66dd9a3ca859c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667918"
---
# <a name="project-settings-type-mapping-sybasetosql"></a>專案設定 (類型對應) (SybaseToSQL)
類型對應 頁面**專案設定** 對話方塊中包含自訂 SSMA 如何轉換成的 Sybase Adaptive Server Enterprise (ASE) 資料類型的設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別。  
  
類型對應 頁面位於**專案設定**並**預設專案設定**對話方塊。  
  
-   若要指定的型別對應設定為所有未來的 SSMA 專案，在**工具**功能表上，選取**預設專案設定**，選取 移轉專案類型，其設定被要求檢視或從變更**移轉目標版本**下拉式清單，然後選取**型別對應**左窗格的底部。  
  
-   若要指定目前的專案中，設定**工具**功能表上，選取**專案設定**，然後選取**型別對應**左窗格的底部。  
  
## <a name="options"></a>選項  
**來源類型**  
對應的資料類型 ASE。  
  
**目標類型**  
目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定 ASE 資料類型的資料類型。  
  
請參閱下節以取得預設 SSMA for Sybase 類型對應中的資料表。  
  
**[加入]**  
按一下以新增的資料類型對應清單。  
  
**編輯**  
按一下以編輯選取的資料類型對應清單中。  
  
**移除**  
按一下即可從對應清單中移除選取的資料類型對應。  
  
**重設為預設值**  
按一下以重設 SSMA 的預設值的類型對應清單。  
  
## <a name="default-type-mapping"></a>預設型別對應  
下表包含 ASE 之間的預設型別對應和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別。  
  
|ASE 資料類型|SQL Server 資料類型|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**binary[\*..8000]**|**binary[\*]**|  
|**binary[8001..\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**char varying[\*..8000]**|**varchar[\*]**|  
|**char varying[8001..\*]**|**varchar(max)**|  
|**char[\*..8000]**|**char[\*]**|  
|**char[8001..\*;]**|**varchar(max)**|  
|**character**|**char**|  
|**可變長度字元**|**varchar**|  
|**character varying[\*..8000]**|**varchar[\*]**|  
|**character varying[8001..\*]**|**varchar(max)**|  
|**character[\*..8000]**|**char[\*]**|  
|**character[8001..\*]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2[3]**|  
|**dec**|**decimal**|  
|**dec[\*..\*]**|**decimal[\*]**|  
|**dec[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**decimal[\*..\*]**|**decimal[\*]**|  
|**decimal[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**雙精度**|**float[53]**|  
|**float**|**float[53]**|  
|**float[\*..15]**|**float[24]**|  
|**float[16..\*]**|**float[53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**nvarchar[255]**|  
|**money**|**money**|  
|**national char**|**nchar**|  
|**national char [\*...4000]**|**nchar[\*]**|  
|**national char varying**|**nvarchar**|  
|**national char varying [\*...4000]**|**nvarchar[\*]**|  
|**national char varying [4001...\*]**|**nvarchar(max)**|  
|**national char [4001...\*]**|**nvarchar(max)**|  
|**國家字元集**|**nchar**|  
|**國家字元集 [\*...4000]**|**nchar[\*]**|  
|**國家字元集 [4001...\*]**|**nvarchar(max)**|  
|**不同的國家字元集**|**nvarchar**|  
|**不同的國家字元集 [\*...4000]**|**nvarchar[\*]**|  
|**不同的國家字元集 [4001...\*]**|**nvarchar(max)**|  
|**national varchar**|**nvarchar**|  
|**national varchar[\*..4000]**|**nvarchar[\*]**|  
|**national varchar[4001..\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar 不同**|**nvarchar**|  
|**nchar varying[\*..4000]**|**nvarchar[\*]**|  
|**nchar varying[4001..\*]**|**nvarchar(max)**|  
|**nchar[\*..4000]**|**nchar[\*]**|  
|**nchar[4001..\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**numeric[\*..\*]**|**numeric[\*]**|  
|**numeric[\*..\*][\*..\*]**|**numeric[\*][\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar[\*..4000]**|**nvarchar[\*]**|  
|**nvarchar[4001..\*]**|**nvarchar(max)**|  
|**real**|**float[24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar[128]**|  
|**sysname[\*..\*]**|**nvarchar[255]**|  
|**text**|**text**|  
|**time**|**time[3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**unichar 不同**|**nvarchar**|  
|**unichar varying[\*..4000]**|**nvarchar[\*]**|  
|**unichar varying[4001..\*]**|**nvarchar(max)**|  
|**unichar[\*..4000]**|**nchar[\*]**|  
|**unichar[4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar[\*..4000]**|**nvarchar[\*]**|  
|**univarchar[4001..\*]**|**nvarchar(max)**|  
|**不帶正負號的 bigint**|**numeric[20][0]**|  
|**不帶正負號的 int**|**bigint**|  
|**不帶正負號的 smallint**|**int**|  
|**不帶正負號的 tinyint**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary[\*..8000]**|**varbinary[\*]**|  
|**varbinary[8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar[\*..8000]**|**varchar[\*]**|  
|**varchar[8001..\*]**|**varchar(max)**|  
  
