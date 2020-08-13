---
title: MSSQLSERVER_50000 | Microsoft Docs
description: 來自嘗試安裝或更新 SQL Server Native Client 的錯誤。 請參閱錯誤的說明及可能的解決方法。
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fbabf983f7866a003b64d8af27c37927b0247dbf
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246552"
---
# <a name="error-mssqlserver_50000-in-sql-server-native-client"></a>SQL Server Native Client 中的錯誤 MSSQLSERVER_50000 
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|產品版本|11.0|  
|事件識別碼|50000|  
|事件來源|SETUP|  
|元件|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client|  
|符號名稱||  
|訊息文字|嘗試讀取檔案 '%.*ls' 時發生網路錯誤。|  
  
## <a name="explanation"></a>說明  
 嘗試在已經安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 而且現有安裝來自從 sqlncli.msi 重新命名之 MSI 檔案的電腦上安裝 (或更新) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client。  
  
## <a name="user-action"></a>使用者動作  
 若要解決這個錯誤，請解除安裝現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 版本。 若要防止這個錯誤發生，請避免從不是名為 sqlncli.msi 的 MSI 檔案安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client。  
  
## <a name="internal-only"></a>僅供內部使用  
  
