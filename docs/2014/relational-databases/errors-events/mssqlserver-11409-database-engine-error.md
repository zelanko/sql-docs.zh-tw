---
title: MSSQLSERVER_11409 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 11409 (Database Engine error)
ms.assetid: 99b71a1c-a72d-4ca9-9d00-4230c9042ba5
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 587b6d15d37e5259ce911c6d278e2d1b48669bc4
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429947"
---
# <a name="mssqlserver11409"></a>MSSQLSERVER_11409
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|11409|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|ALTERCOL_COLSET_DROP|  
|訊息文字|無法卸除資料表 '%.\*ls' 中的資料行集 '%.*ls'，因為資料表包含超過 1025 個資料行。|  
  
## <a name="explanation"></a>說明  
 資料表最多可以包含 1024 個並未指定為疏鬆或計算資料行的資料行。 當疏鬆資料行導致資料表超過 1024 個資料行時，您就必須針對資料表定義資料行集。 參考的資料表具有超過 1024 個資料行，而且您已嘗試移除資料行集。  
  
## <a name="user-action"></a>使用者動作  
 由於目前的資料行位於資料表中，因此您必須保留資料行集。  
  
 若要移除資料行集，請先從資料表中移除資料行，直到沒有超過 1024 個資料行為止。 然後，您就可以移除資料行集。  
  
  
