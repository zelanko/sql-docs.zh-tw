---
title: LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: a7c5ce08-8841-49a3-b252-116807ba469a
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6569c092a9c57f07cbf49b7f932763c5bff13c1e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131506"
---
# <a name="localdberrorinstanceexistswithlowerversion"></a>LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|258|  
|事件來源|SQL Server 本機資料庫執行階段 12.0|  
|元件|本機資料庫執行階段 API|  
|訊息文字|無法以指定的版本建立本機資料庫執行個體。 已存在相同名稱之執行個體，但其版本較指定的版本舊。|  
  
## <a name="explanation"></a>說明  
 指定的執行個體已經存在，但是其版本低於要求的版本。  
  
## <a name="user-action"></a>使用者動作  
 請刪除現有的執行個體，然後再重試作業。  
  
  