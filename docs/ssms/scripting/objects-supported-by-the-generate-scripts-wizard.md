---
title: 指令碼產生精靈支援的物件
description: 查看 [產生和發佈指令碼精靈] 可協助發佈的物件類型。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c9715b44bdd664378842bad70ed4f0d0fea913ab
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901841"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>指令碼產生精靈支援的物件
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [產生和發佈指令碼精靈] 支援 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]支援的物件子集。  
  
## <a name="supported-objects"></a>支援的物件  
 下表將列出 [產生和發佈指令碼精靈] 所支援可發行的物件。  
  
:::row:::
    :::column:::
        應用程式角色
    :::column-end:::
    :::column:::
        資料庫角色
    :::column-end:::
    :::column:::
        結構描述
    :::column-end:::
    :::column:::
        使用者定義彙總
    :::column-end:::
    :::column:::
        檢視*
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        組件
    :::column-end:::
    :::column:::
        DEFAULT 條件約束
    :::column-end:::
    :::column:::
        預存程序*
    :::column-end:::
    :::column:::
        使用者定義資料類型
    :::column-end:::
    :::column:::
        XML 結構描述集合
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        CHECK 條件約束
    :::column-end:::
    :::column:::
        全文檢索目錄
    :::column-end:::
    :::column:::
        同義字
    :::column-end:::
    :::column:::
        使用者定義函數
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        CLR (Common Language Runtime) 預存程序*
    :::column-end:::
    :::column:::
        索引
    :::column-end:::
    :::column:::
        Table
    :::column-end:::
    :::column:::
        使用者定義資料表
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        CLR 使用者定義函數
    :::column-end:::
    :::column:::
        規則
    :::column-end:::
    :::column:::
        使用者**
    :::column-end:::
    :::column:::
        使用者定義型別
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

 *在未經加密的情況下發行。  
  
 **存在資料庫中的任何非系統使用者都將以「角色」的方式發行。  
  
  
