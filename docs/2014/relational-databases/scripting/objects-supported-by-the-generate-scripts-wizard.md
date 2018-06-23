---
title: 指令碼產生精靈支援的物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 071eb2cb-f073-41ca-9f4d-11d3b8803495
caps.latest.revision: 5
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f102fa4366106581c5f3ec4ff141d537531dbaa4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030010"
---
# <a name="objects-supported-by-the-generate-scripts-wizard"></a>指令碼產生精靈支援的物件
  [產生和發佈指令碼精靈] 支援 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]支援的物件子集。  
  
## <a name="supported-objects"></a>支援的物件  
 下表將列出 [產生和發佈指令碼精靈] 所支援可發行的物件。  
  
||||||  
|-|-|-|-|-|  
|應用程式角色|資料庫角色|結構描述|使用者定義彙總|檢視<sup>1</sup>|  
|組件|DEFAULT 條件約束|預存程序<sup>1</sup>|使用者定義資料類型|XML 結構描述集合|  
|CHECK 條件約束|全文檢索目錄|同義字|使用者定義函數||  
|CLR (common language runtime) 預存程序<sup>1</sup>|索引|Table|使用者定義資料表||  
|CLR 使用者定義函數|規則|使用者<sup>2</sup>|使用者定義型別||  
  
 <sup>1</sup>未經加密的情況下發行。  
  
 <sup>2</sup>存在於資料庫中任何非系統使用者會發行為角色。  
  
  