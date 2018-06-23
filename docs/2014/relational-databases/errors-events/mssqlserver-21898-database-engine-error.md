---
title: MSSQLSERVER_21898 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 21898 (Database Engine error)
ms.assetid: 02405b21-3d4e-4c2d-b4b3-d7b1ec05edb4
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2a33000c20c7c8c1399f8f6db653d60841bb7de2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030540"
---
# <a name="mssqlserver21898"></a>MSSQLSERVER_21898
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|21898|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum21898|  
|訊息文字|發行者 '%s' 使用散發資料庫 '%s' 而不是 '%s'，但若要主控發行資料庫 '%s' 必須使用後者。 請在散發者 '%s' 上執行 `sp_changedistpublisher` 以便將發行者所使用的散發資料庫變更為 '%s'。|  
  
## <a name="explanation"></a>說明  
 `sp_validate_redirected_publisher` 在本機散發者上，確認新發行者所使用的散發資料庫與原始發行者所使用的散發資料庫與相同查詢 msdb.dbo.MSdistpublishers。 當這些資料庫不同時，就會傳回此錯誤，讓發行者不適合當做發行者資料庫的主機。  
  
## <a name="user-action"></a>使用者動作  
 請執行 `sp_changedistpublisher` 預存程序，將新發行者的散發資料庫變更為原始發行者所使用的散發資料庫。  
  
> [!NOTE]  
>  如果在發行者的散發者端執行 `sp_changedistpublisher` 時輸入了錯誤的散發資料庫，執行 `sp_adddistpublisher` 便可解決問題。 不過，如果遠端發行者的現有發行集來自使用已識別散發資料庫的另一個發行資料庫，這項變更則不適用。 您必須有系統地移除使用具名散發資料庫的複寫，然後再使用原始發行者的散發資料庫來重新建立複寫，才能讓新的發行者當做適合的主機。  
  
  