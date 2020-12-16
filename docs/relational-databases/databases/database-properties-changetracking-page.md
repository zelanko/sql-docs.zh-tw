---
title: 資料庫屬性 (變更追蹤頁面) | Microsoft 文件
description: 了解如何使用 [資料庫屬性] 對話方塊中 [ChangeTracking] 索引標籤來檢視或修改資料庫的變更追蹤設定。
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.changetracking.f1
ms.assetid: 9b929640-bc62-449b-9b06-b5a77b8cf372
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cfe6b46da2124235f4f2e62e70e13ec486f1b6c0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480299"
---
# <a name="database-properties-changetracking-page"></a>資料庫屬性 (變更追蹤頁面)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  使用此分頁檢視或修改選取之資料庫的變更追蹤設定。 如需此頁面可用之選項的詳細資訊，請參閱[啟用和停用變更追蹤 &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)。  
  
## <a name="options"></a>選項。  
 **變更追蹤**  
 使用此選項啟用或停用資料庫變更追蹤。  
  
 若要啟用變更追蹤，必須先擁有修改資料庫的權限。  
  
 將值設為 [True] 以設定資料庫選項，允許在個別資料表中啟用變更追蹤。  
  
 您也可以使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md)設定變更追蹤。  
  
 **保留週期**  
 指定在資料庫中保存變更追蹤資訊的最小週期。 只有當 **自動清除** 值為 **True** 時，才會移除資料。  
  
 預設值為 2。  
  
 **保留週期單位**  
 指定「保留週期」值的單位。 您可以選取 [日]、[小時] 或 [分鐘]。 預設值為 [日]。  
  
 最小保留週期是 1 分鐘。 沒有最大保留週期。  
  
 **自動清除**  
 指出在經過了指定的保留週期後，是否要自動清除變更追蹤資訊。  
  
 如啟用 [自動清除]，會將所有先前自訂的保留週期重設為預設保留週期：2 日。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)  
  
