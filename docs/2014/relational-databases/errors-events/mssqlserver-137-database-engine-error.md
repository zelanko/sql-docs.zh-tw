---
title: MSSQLSERVER_137 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2eaaadc4e1cc1f2f360fe3d45e2dea4c082b7b76
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62915685"
---
# <a name="mssqlserver137"></a>MSSQLSERVER_137
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|137|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|P_SCALAR_VAR_NOTFOUND|  
|訊息文字|必須宣告純量變數 "%.*ls"。|  
  
## <a name="explanation"></a>說明  
 當您在 SQL 指令碼中使用某個變數，但卻沒有先宣告該變數時，就會發生這個錯誤。 下列範例會針對 SET 和 SELECT 陳述式傳回錯誤 137，因為未宣告 **@mycol**。  
  
 SET @mycol = 'ContactName';  
  
 SELECT @mycol;  
  
 導致這個錯誤的其中一個更複雜原因包括使用了在 EXECUTE 陳述式外部宣告的變數。 例如，在 SELECT 陳述式中指定的變數 **@mycol** 是 SELECT 陳述式的本機變數。因此，這個變數就位於 EXECUTE 陳述式外部。  
  
 USE AdventureWorks2012;  
  
 GO  
  
 DECLARE @mycol nvarchar(20);  
  
 SET @mycol = 'Name';  
  
 EXECUTE ('SELECT @mycol FROM Production.Product;');  
  
## <a name="user-action"></a>使用者動作  
 請確認在 SQL 指令碼中使用的任何變數都已經過宣告，然後再用於指令碼的其他位置。  
  
 重寫指令碼，讓它不會在 EXECUTE 陳述式中參考在該陳述式外部宣告的變數。 例如：  
  
 USE AdventureWorks2012;  
  
 GO  
  
 DECLARE @mycol nvarchar(20) ;  
  
 SET @mycol = 'Name';  
  
 EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';) ;  
  
## <a name="see-also"></a>另請參閱  
 [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)   
 [SET 陳述式 &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statements-transact-sql)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)  
  
  
