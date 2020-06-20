---
title: 選項（查詢結果-SQL Server-多伺服器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqleditors.multiserverresultssettings
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLMultiServerResults
ms.assetid: d6768bd8-9cb5-4606-a726-a33a1df9e1bb
author: rothja
ms.author: jroth
ms.openlocfilehash: 8273ad5edc65dd7351533209e9fa670c49f75f7a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929979"
---
# <a name="options-query-results-sql-server-multi-server"></a>選項 (查詢結果-SQL Server-多伺服器)
  當您同時查詢多部伺服器時，使用這個頁面可指定用來顯示結果集的選項。 合併結果會將所有伺服器的結果集結合到單一結果集內。 合併結果時，要回應的第一部伺服器會設定結果集的結構描述。 若要合併結果集，此查詢必須傳回每一部伺服器中具有相同資料行名稱的相同資料行數。 當合併結果時，會針對不符合結構描述 (資料行計數和資料行名稱) 的每一部伺服器顯示一則訊息 (該結構描述是由第一部傳回結果的伺服器所傳回)。  
  
 當您不要合併結果時，第一部伺服器中的結果集將會顯示在它自己的方格中，而且有它自己的結構描述。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 **合併結果**  
 選取此核取方塊可將幾部伺服器中的結果集結合到相同方格內。  
  
 **將伺服器名稱加入結果**  
 選取此核取方塊可包含另一個資料行，此資料行會提供產生每一個資料列的伺服器名稱。  
  
 **將登入名稱加入結果**  
 選取此核取方塊可包含另一個資料行，此資料行所提供的登入是用來連接提供每一個資料列的伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [建立中央管理伺服器和伺服器群組 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)   
 [同時針對多部伺服器執行陳述式 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/execute-statements-against-multiple-servers-simultaneously.md)  
  
  
