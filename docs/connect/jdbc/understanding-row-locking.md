---
description: 了解資料列鎖定
title: 了解資料列鎖定 | Microsoft Docs
ms.custom: ''
ms.date: 12/08/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 63c76a2f-f2b9-461f-8904-acbda0169ac3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e5305f3feaa80d0a83dd1e7bfd97088492608ae5
ms.sourcegitcommit: 7f76975c29d948a9a3b51abce564b9c73d05dcf0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2020
ms.locfileid: "96901056"
---
# <a name="understanding-row-locking"></a>了解資料列鎖定

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料列鎖定。 這些鎖定會針對同時在資料庫中執行修改的多位使用者實作並行控制。 根據預設，交易和鎖定會針對每一個連接進行管理。 例如，如果應用程式開啟兩個 JDBC 連接，一個連接所取得的鎖定無法與另一個連接共用。 這兩個連接都無法取得會與另一個連接所保留之鎖定產生衝突的鎖定。

> [!NOTE]  
> 如果有使用資料列鎖定，提取緩衝區中的所有資料列都會遭到鎖定，因此，非常大的提取大小設定可能會影響並行。

鎖定的使用是為確保交易完整性與資料庫一致性。 鎖定可防止使用者讀取由其他使用者變更的資料，以及防止多個使用者同時變更相同的資料。 如果沒有使用鎖定，資料庫中的資料可能會變成邏輯上不正確，而且根據該資料執行的查詢可能會產生非預期的結果。

> [!NOTE]  
> 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中資料列鎖定的詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書：[＜[!INCLUDE[ssDE](../../includes/ssde_md.md)] 中的鎖定＞](../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md#Lock_Engine)。

## <a name="see-also"></a>另請參閱

[使用 JDBC 驅動程式管理結果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)
