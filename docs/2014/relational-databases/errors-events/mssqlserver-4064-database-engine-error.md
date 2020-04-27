---
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69332b6d2830c53d5a3f9956443d123fd52485b3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62868023"
---
# <a name="mssqlserver_4064"></a>MSSQLSERVER_4064
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|4064|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DB_UFAIL_FATAL|  
|訊息文字|無法開啟使用者預設資料庫。 登入失敗。|  
  
## <a name="explanation"></a>說明  
 由於預設資料庫發生問題，SQL Server 登入無法連接。 可能是資料庫本身無效，或是登入在資料庫上沒有 CONNECT 權限。  
  
## <a name="user-action"></a>使用者動作  
 使用 ALTER LOGIN 變更登入的預設資料庫。 授與 CONNECT 權限給登入。  
  
  
