---
title: MSSQLSERVER_1101 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1101 (Database Engine error)
ms.assetid: d63b67d5-59f5-4f77-904e-5ba67f2dd850
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce6210f9ab083315fdd99af5c7559a6b98300644
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553943"
---
# <a name="mssqlserver_1101"></a>MSSQLSERVER_1101
    
## <a name="details"></a>詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1101|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|NOALLOCPG|  
|訊息文字|檔案群組中的磁碟空間不足，無法為資料庫 '%.*ls' 配置新的頁面，檔案群組：'%.\*ls'。 請卸除檔案群組中的物件、將其他檔案加入檔案群組，或將檔案群組中現有檔案設定為自動成長，以產生必要的空間。|  
  
## <a name="explanation"></a>說明  
 檔案群組中沒有可用的磁碟空間。  
  
## <a name="user-action"></a>使用者動作  
 下列動作可以在檔案群組中提供可用的空間。  
  
-   開啟自動成長功能。  
  
-   加入更多檔案到檔案中。  
  
-   卸除檔案群組中不需要的索引或資料表，以釋出磁碟空間。  
  
  
