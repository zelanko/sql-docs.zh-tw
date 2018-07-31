---
title: 使用者定義型別 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72dca79e295f54d4c01421ef79408008bd559210
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38039137"
---
# <a name="user-defined-types"></a>使用者定義型別
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用者定義類型 (UDT) 是在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 中引進，可讓開發人員將 Common Language Runtime (CLR) 物件儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 資料庫中來擴充伺服器的純量類別系統。 UDT 可包含多個項目並可具有不同的行為，與只含單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 系統資料類型的傳統別名資料類型有所不同。 在過去，UDT 的大小上限為 8 KB。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] 中，大於 64 KB 的 UDT 已經新增支援。 從 3.0 版開始，當您指定 UserDefined 格式時，JDBC 驅動程式也支援大於 64 KB 的 UDT。  
  
 小於或等於 8,000 個位元組的 UDT 行為並沒有任何變更，但是支援較大的 UDT，而且會將其大小報告為「無限制」。  
  
## <a name="see-also"></a>另請參閱  
 [了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
