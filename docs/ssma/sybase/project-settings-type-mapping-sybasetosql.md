---
description: 專案設定 (類型對應) (SybaseToSQL)
title: 專案設定 (類型對應)  (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 99ab880b69d2c06d462ed42ca0a2529ba6bf7bc2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372114"
---
# <a name="project-settings-type-mapping-sybasetosql"></a>專案設定 (類型對應) (SybaseToSQL)
[ **專案設定** ] 對話方塊的 [型別對應] 頁面包含的設定，可自訂 SSMA 如何將 Sybase 適應性 Server ENTERPRISE (ASE) 資料類型轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。  
  
[類型對應] 頁面可在 [ **專案設定** ] 和 [ **預設專案設定** ] 對話方塊中使用。  
  
-   若要指定所有未來 SSMA 專案的型別對應設定，請在 [ **工具** ] 功能表上，選取 [ **預設專案設定**]，選取 [遷移專案類型]，需要從 [ **遷移目標版本** ] 下拉式清單中查看或變更設定，然後選取左窗格底部的 [ **類型對應** ]。  
  
-   若要指定目前專案的設定，請在 [ **工具** ] 功能表上選取 [ **專案設定**]，然後選取左窗格底部的 [ **類型對應** ]。  
  
## <a name="options"></a>選項。  
**來源類型**  
對應的 ASE 資料類型。  
  
**目標型別**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定 ASE 資料類型的目標資料類型。  
  
請參閱下一節中的資料表，以取得 Sybase 類型對應的預設 SSMA。  
  
**加入**  
按一下以將資料類型加入至對應清單。  
  
**編輯**  
按一下即可編輯 [對應] 清單中所選取的資料類型。  
  
**移除**  
按一下即可從 [對應] 清單中移除選取的資料類型對應。  
  
**重設為預設值**  
按一下以將類型對應清單重設為 SSMA 預設值。  
  
## <a name="default-type-mapping"></a>預設型別對應  
下表包含 ASE 和資料類型之間的預設型別對應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
|ASE 資料類型|SQL Server 資料類型|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**binary**|**binary**|  
|**binary [ \* .。。8000]**|**binary [ \* ]**|  
|**binary [8001 ... \* ]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**char 變化 [ \* .。。8000]**|**Varchar [ \* ]**|  
|**char 變化 [8001 ... \* ]**|**varchar(max)**|  
|**char [ \* .。。8000]**|**char [ \* ]**|  
|**char [8001 ... \* ]**|**varchar(max)**|  
|**字元**|**char**|  
|**character varying**|**varchar**|  
|**字元差異 [ \* .。。8000]**|**Varchar [ \* ]**|  
|**字元差異 [8001 ... \* ]**|**varchar(max)**|  
|**字元 [ \* .。8000]**|**char [ \* ]**|  
|**字元 [8001 ... \* ]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2 [3]**|  
|**12 月**|**decimal**|  
|**dec [ \* ... \* ]**|**decimal [ \* ]**|  
|**dec [ \* ... \* ][\*..\*]**|**decimal [ \* ] [ \* ]**|  
|**decimal**|**decimal**|  
|**decimal [ \* ... \* ]**|**decimal [ \* ]**|  
|**decimal [ \* ... \* ][\*..\*]**|**decimal [ \* ] [ \* ]**|  
|**雙精確度**|**float [53]**|  
|**float**|**float [53]**|  
|**float [ \* .。。長**|**float [24]**|  
|**float [16 ... \* ]**|**float [53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**Nvarchar [255]**|  
|**money**|**money**|  
|**國家/地區字元**|**nchar**|  
|**國家字元 [ \* .。4000]**|**Nchar [ \* ]**|  
|**國家字元變動**|**nvarchar**|  
|**國家字元變化 [ \* .。。4000]**|**Nvarchar [ \* ]**|  
|**國家字元變化 [4001 ... \* ]**|**nvarchar(max)**|  
|**國家字元 [4001 ... \* ]**|**nvarchar(max)**|  
|**國家字元**|**nchar**|  
|**國家字元 [ \* .。4000]**|**Nchar [ \* ]**|  
|**國家字元 [4001.. \* ]**|**nvarchar(max)**|  
|**國家字元變動**|**nvarchar**|  
|**國際字元不同 [ \* .。。4000]**|**Nvarchar [ \* ]**|  
|**國際字元不同 [4001 ... \* ]**|**nvarchar(max)**|  
|**全國 Varchar**|**nvarchar**|  
|**全國 Varchar [ \* .。。4000]**|**Nvarchar [ \* ]**|  
|**全國 Varchar [4001 ... \* ]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**Nchar 變化**|**nvarchar**|  
|**Nchar 變化 [ \* .。。4000]**|**Nvarchar [ \* ]**|  
|**Nchar 不同 [4001 ... \* ]**|**nvarchar(max)**|  
|**Nchar [ \* .。。4000]**|**Nchar [ \* ]**|  
|**Nchar [4001 ... \* ]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**數值 [ \* ... \* ]**|**數值 [ \* ]**|  
|**數值 [ \* ... \* ][\*..\*]**|**數值 [ \* ] [ \* ]**|  
|**nvarchar**|**nvarchar**|  
|**Nvarchar [ \* .。。4000]**|**Nvarchar [ \* ]**|  
|**Nvarchar [4001 ... \* ]**|**nvarchar(max)**|  
|**real**|**float [24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**Nvarchar [128]**|  
|**sysname [ \* ... \* ]**|**Nvarchar [255]**|  
|**text**|**text**|  
|**time**|**時間 [3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**則 unichar 會**|**nchar**|  
|**則 unichar 會變化**|**nvarchar**|  
|**則 unichar 會變化 [ \* .。。4000]**|**Nvarchar [ \* ]**|  
|**則 unichar 會變化 [4001 ... \* ]**|**nvarchar(max)**|  
|**則 unichar 會 [ \* .。。4000]**|**Nchar [ \* ]**|  
|**則 unichar 會 [4001 ... \* ]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**uniVarchar**|**nvarchar**|  
|**uniVarchar [ \* .。。4000]**|**Nvarchar [ \* ]**|  
|**uniVarchar [4001 ... \* ]**|**nvarchar(max)**|  
|**不帶正負號的 Bigint**|**數值 [20] [0]**|  
|**不帶正負號的整數**|**bigint**|  
|**不帶正負號的 Smallint**|**int**|  
|**不帶正負號的 Tinyint**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**Varbinary [ \* .。。8000]**|**Varbinary [ \* ]**|  
|**Varbinary [8001 ... \* ]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**Varchar [ \* .。。8000]**|**Varchar [ \* ]**|  
|**Varchar [8001 ... \* ]**|**varchar(max)**|  
  
