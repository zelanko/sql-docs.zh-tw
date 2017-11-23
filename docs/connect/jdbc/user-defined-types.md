---
title: "使用者定義型別 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ccd5c353efd622fa406bfeb5c5b9c44c9546364b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="user-defined-types"></a>使用者定義型別
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  使用者定義型別 (Udt) 中導入[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]可讓開發人員透過儲存在 common language runtime (CLR) 物件來擴充伺服器的純量類型系統[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。 Udt 可包含多個項目，並可以具有行為，與不同的傳統別名資料型別，只包含單一[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]系統資料類型。 在過去，UDT 的大小上限為 8 KB。 在[!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]，大於 64 kb 的 Udt 已經加入支援。 從 3.0 版開始，當您指定 UserDefined 格式時，JDBC 驅動程式也支援大於 64 KB 的 UDT。  
  
 小於或等於 8,000 個位元組的 UDT 行為並沒有任何變更，但是支援較大的 UDT，而且會將其大小報告為「無限制」。  
  
## <a name="see-also"></a>請參閱＜  
 [了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
