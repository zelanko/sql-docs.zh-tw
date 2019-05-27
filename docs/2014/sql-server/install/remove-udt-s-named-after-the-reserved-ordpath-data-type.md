---
title: 移除 UDT&#39;s 名為保留的 ORDPATH 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 474e910a-6abb-4e28-acc2-055338c011d4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3ee155c70a8b10d4437d6b2f374c8b9497bf3faa
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092915"
---
# <a name="remove-udt39s-named-after-the-reserved-ordpath-data-type"></a>移除 UDT&#39;s 名為保留的 ORDPATH 資料類型
  Upgrade Advisor 偵測到依據為 `ORDPATH` 資料類型保留之詞彙所命名的使用者定義型別 (UDT)。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 用於內建資料類型的詞彙不應該當做 Common Language Runtime (CLR) 或別名 UDT 的名稱使用。  
  
## <a name="corrective-action"></a>更正動作  
 請移除依據此資料類型所命名的 UDT，然後使用未保留的名稱重新建立 UDT。  
  
## <a name="external-resources"></a>外部資源  
 [建立使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
