---
title: "指令碼產生精靈支援的物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87fde29aab8338f096d2132b13011e44fcf96014
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>指令碼產生精靈支援的物件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] [產生和發佈指令碼精靈] 支援 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 支援的物件子集。  
  
## <a name="supported-objects"></a>支援的物件  
 下表將列出 [產生和發佈指令碼精靈] 所支援可發行的物件。  
  
||||||  
|-|-|-|-|-|  
|應用程式角色|資料庫角色|結構描述|使用者定義彙總|檢視*|  
|組件|DEFAULT 條件約束|預存程序*|使用者定義資料類型|XML 結構描述集合|  
|CHECK 條件約束|全文檢索目錄|同義字|使用者定義函數||  
|CLR (Common Language Runtime) 預存程序*|索引|Table|使用者定義資料表||  
|CLR 使用者定義函數|規則|使用者**|使用者定義型別||  
  
 *在未經加密的情況下發行。  
  
 **存在資料庫中的任何非系統使用者都將以「角色」的方式發行。  
  
  
