---
title: 專案設定（類型對應）（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d7b16bdf3717fa14f91af41663cbd65365eac52a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028657"
---
# <a name="project-settings-type-mapping-sybasetosql"></a>專案設定 (類型對應) (SybaseToSQL)
[**專案設定**] 對話方塊的 [類型對應] 頁面包含自訂 SSMA 如何將 Sybase 調適型伺服器 ENTERPRISE （ASE）資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類型轉換成資料類型的設定。  
  
[類型對應] 頁面可在 [**專案設定**] 和 [**預設專案設定**] 對話方塊中取得。  
  
-   若要指定所有未來 SSMA 專案的類型對應設定，請在 [**工具**] 功能表上，選取 [**預設專案設定**]，然後選取 [遷移] [**目標版本**] 下拉式選時需要查看或變更設定的 [遷移專案類型]，然後選取左窗格底部的 [**類型對應**]。  
  
-   若要指定目前專案的設定，請在 [**工具**] 功能表上，選取 [**專案設定**]，然後選取左窗格底部的 [**類型對應**]。  
  
## <a name="options"></a>選項。  
**來源類型**  
對應的 ASE 資料類型。  
  
**目標類型**  
指定 ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型的目標資料類型。  
  
如需 Sybase 類型對應的預設 SSMA，請參閱下一節中的表格。  
  
**加入**  
按一下即可將資料類型加入至 [對應] 清單。  
  
**編輯**  
按一下即可編輯 [對應] 清單中選取的資料類型。  
  
**移除**  
按一下即可從 [對應] 清單中移除選取的資料類型對應。  
  
**重設為預設值**  
按一下即可將 [類型對應] 清單重設為 SSMA 預設值。  
  
## <a name="default-type-mapping"></a>預設型別對應  
下表包含 ASE 與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型之間的預設型別對應。  
  
|ASE 資料類型|SQL Server 資料類型|  
|-----------------|------------------------|  
|**Bigint**|**Bigint**|  
|**binary**|**binary**|  
|**binary [\*.。8000]**|**binary [\*]**|  
|**binary [8001 ...\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char 改變**|**varchar**|  
|**char 改變 [\*.。8000]**|**Varchar [\*]**|  
|**char 改變 [8001 ...\*]**|**varchar(max)**|  
|**char [\*.。8000]**|**char [\*]**|  
|**char [8001 ...\*]**|**varchar(max)**|  
|**字母**|**char**|  
|**字元變動**|**varchar**|  
|**字元變動 [\*.。8000]**|**Varchar [\*]**|  
|**字元變動 [8001 ...\*]**|**varchar(max)**|  
|**字元 [\*.。8000]**|**char [\*]**|  
|**字元 [8001 ...\*]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2 [3]**|  
|**十進位**|**decimal**|  
|**dec [\*.。\*]**|**decimal [\*]**|  
|**dec [\*.。\*][\*..\*]**|**decimal [\*] [\*]**|  
|**decimal**|**decimal**|  
|**decimal [\*.。\*]**|**decimal [\*]**|  
|**decimal [\*.。\*][\*..\*]**|**decimal [\*] [\*]**|  
|**雙精度**|**float [53]**|  
|**float**|**float [53]**|  
|**float [\*.。次**|**float [24]**|  
|**float [16 ...\*]**|**float [53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**Nvarchar [255]**|  
|**money**|**money**|  
|**國家/地區**|**nchar**|  
|**國家 char [\*.。4000]**|**Nchar [\*]**|  
|**國家/地區 char 改變**|**nvarchar**|  
|**國家 char 改變 [\*.。4000]**|**Nvarchar [\*]**|  
|**國家/地區不同 [4001\*]**|**nvarchar(max)**|  
|**國家字元 [4001 ...\*]**|**nvarchar(max)**|  
|**國家字元**|**nchar**|  
|**國家字元 [\*.。4000]**|**Nchar [\*]**|  
|**國家字元 [4001 ...\*]**|**nvarchar(max)**|  
|**國家字元變動**|**nvarchar**|  
|**國家字元變動 [\*.。4000]**|**Nvarchar [\*]**|  
|**國家字元變動 [4001 ...\*]**|**nvarchar(max)**|  
|**全國 Varchar**|**nvarchar**|  
|**國家 Varchar [\*.。4000]**|**Nvarchar [\*]**|  
|**全國 Varchar [4001 ...\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**Nchar 改變**|**nvarchar**|  
|**Nchar 改變 [\*.。4000]**|**Nvarchar [\*]**|  
|**Nchar 改變 [4001 ...\*]**|**nvarchar(max)**|  
|**Nchar [\*.。4000]**|**Nchar [\*]**|  
|**Nchar [4001 ...\*]**|**nvarchar(max)**|  
|**數值**|**數值**|  
|**數值 [\*.。\*]**|**數值 [\*]**|  
|**數值 [\*.。\*][\*..\*]**|**數值 [\*] [\*]**|  
|**nvarchar**|**nvarchar**|  
|**Nvarchar [\*.。4000]**|**Nvarchar [\*]**|  
|**Nvarchar [4001 ...\*]**|**nvarchar(max)**|  
|**即時**|**float [24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**SMALLMONEY**|**SMALLMONEY**|  
|**sysname**|**Nvarchar [128]**|  
|**sysname [\*.。。\*]**|**Nvarchar [255]**|  
|**text**|**text**|  
|**time**|**時間 [3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**unichar 改變**|**nvarchar**|  
|**unichar 改變 [\*.。4000]**|**Nvarchar [\*]**|  
|**unichar 改變 [4001 ...\*]**|**nvarchar(max)**|  
|**unichar [\*.。。4000]**|**Nchar [\*]**|  
|**unichar [4001 ...\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**uniVarchar**|**nvarchar**|  
|**uniVarchar [\*.。。4000]**|**Nvarchar [\*]**|  
|**uniVarchar [4001 ...\*]**|**nvarchar(max)**|  
|**不帶正負號的 Bigint**|**數值 [20] [0]**|  
|**不帶正負號的整數**|**Bigint**|  
|**不帶正負號的 Smallint**|**int**|  
|**不帶正負號的 Tinyint**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**Varbinary [\*.。8000]**|**Varbinary [\*]**|  
|**Varbinary [8001 ...\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**Varchar [\*.。8000]**|**Varchar [\*]**|  
|**Varchar [8001 ...\*]**|**varchar(max)**|  
  
