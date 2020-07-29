---
title: 訂閱驗證選項 (合併式)
description: 說明 SQL Server Management Studio (SSMS) 內的 [訂閱驗證選項] 對話方塊。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.mergeoptions.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: 4958c4ab-2025-42ce-b836-6fb4e9e6f24d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 497282dbdc0710f732c10f9e06abbffc40d4d046
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87111995"
---
# <a name="subscription-validation-options-merge-subscriptions"></a>訂閱驗證選項 (合併訂閱)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  使用 **[訂閱驗證選項]** 對話方塊來指定驗證應該只使用資料列計數，或使用資料列計數與二進位總和檢查碼。  
  
## <a name="options"></a>選項。  
 **只確認資料列計數**  
 選取以驗證訂閱者端之資料表的資料列數目是否與發行者端之資料表的資料列數目相同。 此方法不會驗證資料列的內容是否相符。 資料列計數驗證提供一種輕量型驗證方法，可讓您發現資料中的問題。  
  
 **確認資料列計數並比較總和檢查碼，來確認資料列資料**  
 除了統計「發行者」與「訂閱者」上的資料列數量之外，也會使用二進位總和檢查碼演算法計算所有資料的總和檢查碼。 如果資料列計數失敗，就不會執行總和檢查碼。 這個選項對於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] 無效。  
  
## <a name="see-also"></a>另請參閱  
 [驗證訂閱者端的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [驗證複寫的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
