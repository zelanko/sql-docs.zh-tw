---
title: MSSQLSERVER_50000 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f872d7d0a2495e747ae0b3d63997f7270c585c53
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-native-client-error-mssqlserver50000"></a>SQL Server Native Client 錯誤 MSSQLSERVER_50000
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
  
