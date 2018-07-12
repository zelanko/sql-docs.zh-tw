---
title: MSSQLSERVER_2518 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 2518 (Database Engine error)
ms.assetid: 54a13abc-4c33-43f0-b55d-e2e74a1381c8
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a4fc661059240f626c9f61e3b81f4a80350680fa
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425058"
---
# <a name="mssqlserver2518"></a>MSSQLSERVER_2518
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|2518|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_NO_EXPRESSION_EVAL_CLR_DISABLED|  
|訊息文字|物件識別碼 O_ID (物件 "O_NAME"): 無法檢查此物件的計算資料行和使用者自訂類型，因為 Common Language Runtime (CLR) 已停用。|  
  
## <a name="explanation"></a>說明  
 這項參考用訊息指出查詢處理器無法提供 DBCC 與內部物件，以便評估計算資料行和 Common Language Runtime (CLR) 使用者自訂類型。 發生這個問題的原因是因為其中一個資料行包含 CLR，但是 CLR 並未啟用。 該內部物件涵蓋所有資料行。 因此，無法評估單一資料行也會造成無法建立內部物件的結果。 這表示 DBCC 不會在檢查索引和基底資料表的一致性時檢查計算資料行的正確性，或是使用這些計算資料行。  
  
## <a name="user-action"></a>使用者動作  
 啟用 CLR，然後重新執行 DBCC 陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [啟用 CLR 整合](../clr-integration/clr-integration-enabling.md)  
  
  
