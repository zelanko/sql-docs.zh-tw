---
title: MSSQLSERVER_2570 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 2570 (Database Engine error)
ms.assetid: 29800aa9-81aa-4371-992c-487dbb617f46
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8ae42b008eba97f129510c641e748528dae26bdf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver2570"></a>MSSQLSERVER_2570
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2570|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_COLUMN_VALUE_OUT_OF_RANGE|  
|訊息文字|頁面 P_ID，物件識別碼 O_ID 中的位置 S_ID，索引識別碼 I_ID，分割區識別碼 PN_ID，配置單位識別碼 A_ID (類型 TYPE)。 資料行 COLUMN_NAME 值超出資料類型 "DATATYPE" 的範圍。 請將資料行更新為合法的值。|  
  
## <a name="explanation"></a>說明  
包含在指定之資料行中的資料行值超出資料行資料類型可能值的範圍。  
  
## <a name="user-action"></a>使用者動作  
這是無法修復的錯誤。 請將資料行更新為資料行之資料類型範圍內的值，並重新執行命令。  如需詳細資訊，請參閱這篇知識庫文章：[923247](http://support.microsoft.com/kb/923247)。  
  
## <a name="see-also"></a>另請參閱  
[UPDATE &#40;Transact-SQL&#41;](~/t-sql/queries/update-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](~/t-sql/data-types/data-types-transact-sql.md)  
  
