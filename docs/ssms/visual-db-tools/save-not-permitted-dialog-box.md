---
description: 儲存 (不允許) 對話方塊
title: 儲存 (不允許) 對話方塊
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.table.tablerecreatenosave.f1
ms.assetid: 7efda8e3-739f-4c97-a497-b8808a0acbea
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 868925a64b24ab7f55551a691b4677a658082725
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88369084"
---
# <a name="save-not-permitted-dialog-box"></a>儲存 (不允許) 對話方塊
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
[儲存]**** \(不允許) 對話方塊會警告您不允許儲存變更，因為您所做的變更需要卸除及重新建立所列出的資料表。  
  
下列動作可能需要重新建立資料表：  
  
-   將新的資料行加入資料表的中間  
  
-   卸除資料行  
  
-   變更資料行的 Null 屬性  
  
-   變更資料行的順序  
  
-   變更資料行的資料類型  
  
若要變更這個選項，請在 [工具]**** 功能表上按一下 [選項]****，展開 [設計工具]****，然後按一下 [資料表和資料庫設計工具]****。 選取或清除 [防止儲存需要資料表重建的變更]**** 核取方塊。  
  
