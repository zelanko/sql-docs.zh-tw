---
title: MSSQLSERVER_50000 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc7e8eea45c9a08249f7efd6d8ec66c5a0a80c0f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sql-server-native-client-error-mssqlserver50000"></a>SQL Server Native Client 錯誤 MSSQLSERVER_50000
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
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
  
